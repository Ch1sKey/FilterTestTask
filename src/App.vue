<template>
  <v-app>
    <div class="wrapper">
      <header>
        <h1 class="main-title">Lorem ipsum dolor sit</h1>
      </header>
      <main>
        <div class="filters">
          <div class="filters__item">
            <FilterInputSelector
              ref="switchers"
              @input="switchersInput"
              :title="'Комнаты'"
              :values='sizes'
            />
          </div>
          <div class="filters__item">
            <FilterInputRange
              ref="floorRange"
              @input="floorsRangeInput"
              :range="rangeFloors"
              :title="'Этаж'"
            />
          </div>
          <div class="filters__item">
            <FilterInputRange
              ref="squareRange"
              @input="squareRangeInput"
              :range="rangeSquare"
              :title="'Площадь'"
              :units="'м<sup>2</sup>'"
            />
          </div>
          <div class="filters__item">
            <FilterInputRange
              ref="priceRange"
              @input="priceRangeInput" 
              :step="0.1" 
              :range="rangePrice" 
              :title="'Стоимость'"
              :units="'млн. р.'"
            />
          </div>
          <div class="filters__buttons">
            <button @mouseup="$event.target.blur()" @click="applyFilter" class="button button_main">Применить</button>
            <button @mouseup="$event.target.blur()" @click="dropFilter" class="button button_secondary">
              <span>Сбросить фильтр</span>
            </button>
          </div>
        </div>
        <div class="scroll-container-wrapper">
          <div class="scroll-container">
            <ApartmentCard :key='i' :data="item" v-for="(item,i) in filteredData"
            class="scroll-container__item" />
          </div>
        </div>
      </main>
    </div>
  </v-app>
</template>

<script>
import FilterInputSelector from './components/FilterInputSelector'
import FilterInputRange from './components/FilterInputRange'
import ApartmentCard from './components/ApartmentCard'

export default {
  name: 'App',
  components: {
    FilterInputSelector,
    FilterInputRange,
    ApartmentCard
  },
  data() {
    return {
      data: [],
      inputSwitchers: [],
      filteredData: [],
      floorsRangeData: [],
      squareRangeData: [],
      priceRangeData: []
    }
  },
  computed: {
    sizes() {
      return [...new Set(this.data.map(item => item.size))].sort((itemA, itemB) => {
        if(isNaN(parseInt(itemB))) return 1;
        return itemA > itemB ? 1 : -1
      })
    },
    rangeFloors() {
      const min = Math.min(...this.data.map(item => item.floor))
      const max = Math.max(...this.data.map(item => item.floor))
      return [min, max]
    },
    rangeSquare() {
      let min = Math.min(...this.data.map(item => item.square))
      let max = Math.max(...this.data.map(item => item.square))
      min = Math.floor(min)
      max = Math.floor(max)
      return [min, max]      
    },
    rangePrice() {
      let min = Math.min(...this.data.map(item => item.price))
      let max = Math.max(...this.data.map(item => item.price))
      min = this.roundPrice(min)
      max = this.roundPrice(max)
      return [min, max]           
    }
  },
  methods: {
    roundPrice(number) { return Math.floor((number / 1_000_000 + Number.EPSILON) * 10) / 10 },
    floorsRangeInput(rangeData) { this.floorsRangeData = rangeData },
    squareRangeInput(rangeData) { this.squareRangeData = rangeData },
    priceRangeInput(rangeData) { this.priceRangeData = rangeData },
    switchersInput(switchersData) { this.inputSwitchers = switchersData },
    dropFilter() {
      this.$refs["switchers"].setDefault()
      this.$refs["floorRange"].setDefault()
      this.$refs["squareRange"].setDefault()
      this.$refs["priceRange"].setDefault()
    },
    applyFilter() {
      this.filteredData = this.data.filter(item => {
        const floor = item.floor
        const square = Math.floor(item.square)
        const price = this.roundPrice(item.price)
        const floorFilter = floor >= this.floorsRangeData[0] && floor <= this.floorsRangeData[1]
        const squareFilter = square >= this.squareRangeData[0] && square <= this.squareRangeData[1]
        const priceFilter = price >= this.priceRangeData[0] &&  price <= this.priceRangeData[1] 
        const sizesFilter = this.inputSwitchers.includes(item.size)
        return floorFilter && squareFilter && priceFilter && sizesFilter
      })
    }
  },
  mounted() {
    const data = [
      {
        building_id: 73,
        building_name: "1 этап 1а корпуса",
        floor: 10,
        id: 23329,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 2956317,
        rooms: 1,
        size: "XS",
        square: 23.66,
      },
      {
        building_id: 74,
        building_name: "1 этап 1а корпуса",
        floor: 4,
        id: 20822,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 2992701,
        rooms: 1,
        size: "XS",
        square: 23.87,
      },
      {
        building_id: 75,
        building_name: "1 этап 1а корпуса",
        floor: 4,
        id: 20382,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 4952721,
        rooms: 2,
        size: "2k",
        square: 42.87,
      },
      {
        building_id: 75,
        building_name: "1 этап 1а корпуса",
        floor: 4,
        id: 20332,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 8862732,
        rooms: 3,
        size: "3k",
        square: 42.87,
      },
      {
        building_id: 32,
        building_name: "1 этап 1а корпуса",
        floor: 10,
        id: 20328,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 3956317,
        rooms: 1,
        size: "1k",
        square: 24.99,
      },
      {
        building_id: 37,
        building_name: "1 этап 1а корпуса",
        floor: 10,
        id: 20320,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 3956317,
        rooms: 1,
        size: "XS",
        square: 24.99,
      },
      {
        building_id: 17,
        building_name: "1 этап 1а корпуса",
        floor: 10,
        id: 33320,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 5956317,
        rooms: 1,
        size: "2k",
        square: 45.36,
      },
      {
        building_id: 87,
        building_name: "1 этап 1а корпуса",
        floor: 10,
        id: 33320,
        is_studio: 1,
        number: "163",
        plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
        porch: 3,
        price: 9956317,
        rooms: 4,
        size: "4",
        square: 66.60,
      },
    ]
    this.data = [...data, ...data] //8 is too few
    this.$nextTick(() => {
      this.applyFilter()
    })
    
  }
};
</script>
<style src="@/styles/app.css"></style>

<style>
  @import '~@/styles/fonts.css';
  @import '~@/styles/button.css';
</style>
