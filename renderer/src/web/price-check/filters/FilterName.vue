<template>
  <div class="filter-name">
    <button class="px-2 rounded border"
      :class="{ 'border-gray-500': showAsActive, 'border-gray-900': !showAsActive }"
      @click="toggleAccuracy">{{ label }}</button>
    <button v-if="filters.corrupted" class="px-2" @click="corrupted = !corrupted">
      <span v-if="corrupted" class="text-red-500">{{ t('Corrupted') }}</span>
      <span v-else class="text-gray-600">{{ t('Not Corrupted') }}</span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
import { useI18n } from 'vue-i18n'
import type { ParsedItem } from '@/parser'
import type { ItemFilters } from './interfaces'

export default defineComponent({
  name: 'FilterName',
  props: {
    filters: {
      type: Object as PropType<ItemFilters>,
      required: true
    },
    item: {
      type: Object as PropType<ParsedItem>,
      required: true
    }
  },
  setup (props) {
    const { t } = useI18n()

    const label = computed(() => {
      const { filters } = props
      const activeSearch = (filters.searchRelaxed && !filters.searchRelaxed.disabled)
        ? filters.searchRelaxed
        : filters.searchExact

      if (activeSearch.name) {
        return activeSearch.name
      }
      if (activeSearch.baseType) {
        return activeSearch.baseType
      }
      if (activeSearch.category) {
        return t(`Category: ${activeSearch.category}`)
      }

      return '??? Report if you see this text'
    })

    const showAsActive = computed(() => {
      const { filters } = props
      return filters.searchRelaxed?.disabled
    })

    function toggleAccuracy () {
      const { filters } = props
      if (filters.searchRelaxed) {
        filters.searchRelaxed.disabled = !filters.searchRelaxed.disabled
      }
    }

    const corrupted = computed<boolean>({
      get () { return props.filters.corrupted!.value },
      set (value) { props.filters.corrupted!.value = value }
    })

    return {
      t,
      label,
      showAsActive,
      toggleAccuracy,
      corrupted
    }
  }
})
</script>

<style lang="postcss">
.filter-name {
  @apply bg-gray-900 mb-2 rounded;
  line-height: 1.25rem;
  display: flex;
  justify-content: space-between;
}
</style>

<i18n>
{
  "ru": {
    "Corrupted": "Осквернен",
    "Not Corrupted": "Не осквернен",
    "Category: Abyss Jewel": "Категория: Самоцвет Бездны",
    "Category: Amulet": "Категория: Амулет",
    "Category: Belt": "Категория: Пояс",
    "Category: Body Armour": "Категория: Нательная броня",
    "Category: Boots": "Категория: Сапоги",
    "Category: Bow": "Категория: Лук",
    "Category: Claw": "Категория: Коготь",
    "Category: Dagger": "Категория: Кинжал",
    "Category: Fishing Rod": "Категория: Удочка",
    "Category: Flask": "Категория: Флакон",
    "Category: Gloves": "Категория: Перчатки",
    "Category: Helmet": "Категория: Шлем",
    "Category: Jewel": "Категория: Самоцвет",
    "Category: One-Handed Axe": "Категория: Одноручный топор",
    "Category: One-Handed Mace": "Категория: Одноручная булава",
    "Category: One-Handed Sword": "Категория: Одноручный меч",
    "Category: Quiver": "Категория: Колчан",
    "Category: Ring": "Категория: Кольцо",
    "Category: Rune Dagger": "Категория: Рунический кинжал",
    "Category: Sceptre": "Категория: Скипетр",
    "Category: Shield": "Категория: Щит",
    "Category: Staff": "Категория: Посох",
    "Category: Two-Handed Axe": "Категория: Двуручный топор",
    "Category: Two-Handed Mace": "Категория: Двуручная булава",
    "Category: Two-Handed Sword": "Категория: Двуручный меч",
    "Category: Wand": "Категория: Жезл",
    "Category: Warstaff": "Категория: Воинский посох",
    "Category: Cluster Jewel": "Категория: Кластерный самоцвет",
    "Category: Heist Blueprint": "Категория: Чертёж Кражи",
    "Category: Heist Contract": "Категория: Контракт Кражи",
    "Category: Heist Tool": "Категория: Разбойничий инструмент",
    "Category: Heist Brooch": "Категория: Разбойничья брошь",
    "Category: Heist Gear": "Категория: Разбойничьи принадлежности",
    "Category: Heist Cloak": "Категория: Разбойничья накидка",
    "Category: Trinket": "Категория: Украшение"
  },
  "ko": {
    "Corrupted": "타락",
    "Not Corrupted": "",
    "Category: Abyss Jewel": "항목: 심연 주얼",
    "Category: Amulet": "항목: 목걸이",
    "Category: Belt": "항목: 허리띠",
    "Category: Body Armour": "항목: 갑옷",
    "Category: Boots": "항목: 장화",
    "Category: Bow": "항목: 활",
    "Category: Claw": "항목: 클로",
    "Category: Dagger": "항목: 단검",
    "Category: Fishing Rod": "항목: 낚시대",
    "Category: Flask": "항목: 플라스크",
    "Category: Gloves": "항목: 장갑",
    "Category: Helmet": "항목: 투구",
    "Category: Jewel": "항목: 주얼",
    "Category: One-Handed Axe": "항목: 한손 도끼",
    "Category: One-Handed Mace": "항목: 한손 철퇴",
    "Category: One-Handed Sword": "항목: 한손 검",
    "Category: Quiver": "항목: 화살통",
    "Category: Ring": "항목: 반지",
    "Category: Rune Dagger": "항목: 룬 단검",
    "Category: Sceptre": "항목: 셉터",
    "Category: Shield": "항목: 방패",
    "Category: Staff": "항목: 지팡이",
    "Category: Two-Handed Axe": "항목: 양손 도끼",
    "Category: Two-Handed Mace": "항목: 양손 철퇴",
    "Category: Two-Handed Sword": "항목: 양손 검",
    "Category: Wand": "항목: 마법봉",
    "Category: Warstaff": "항목: 전쟁지팡이",
    "Category: Cluster Jewel": "항목: 군 주얼",
    "Category: Heist Blueprint": "항목: 강탈 도면",
    "Category: Heist Contract": "항목: 강탈 계약",
    "Category: Heist Tool": "항목: 강탈 도구",
    "Category: Heist Brooch": "항목: 강탈 브로치",
    "Category: Heist Gear": "항목: 강탈 장비",
    "Category: Heist Cloak": "항목: 강탈 망토",
    "Category: Trinket": "항목: 장신구"
  }
}
</i18n>
