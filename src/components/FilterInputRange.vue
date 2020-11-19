<template>
  <div class="filter-input" role="group" aria-labelledby="id-group-label">
    <div id="id-group-label" class="filter-input__title">{{title}}<span v-html="getUnit"></span></div>
    <div class="filter-input__range-values">
      <input class="filter-input__field"
        :value='currentRange[0] || 0'
        @input="inputRange(0, $event.target.value)" />
      <div class="filter-input__range-values__separator">-</div>
      <input class="filter-input__field"
        :value='currentRange[1] || 0'
        @input="inputRange(1, $event.target.value)"
      />
    </div>
    <v-range-slider
      v-model='currentRange'
      hide-details
      :step="step"
      :min="range[0]"
      :max="range[1]"
    ></v-range-slider>
  </div>
</template>
<script>
export default {
  name: "FilterInputRange",
  props: ["range", "title", "units" , "step"],
  data() {
    return {
      currentRange: [-10, 9],
    }
  },
  computed: {
    getUnit() {
      return this.units ? `, ${this.units}` : ''
    },
  },
  mounted() {
    this.setDefault()
  },
  watch: {
    currentRange(rangeData) {
      this.$emit('input', rangeData)
    }
  },
  methods: {
    setDefault() {
      this.currentRange = this.range
      this.inputRange()
    },
    inputRange(index, value) {
      if(!isNaN(+value)) {
        this.$set(this.currentRange, index, value)
      }
    }
  }
}
</script>
<style>
.v-slider__thumb::before {
  content: '';
  display: none;
}

.v-slider .v-slider__track-container div.v-slider__track-fill {
  background-color: #70D24E !important;
}

.v-slider .v-slider__track-container div.v-slider__track-background {
  background-color: #D8D8D8 !important;
}

.v-slider .v-slider__thumb-container div.v-slider__thumb {
  width: 24px;
  height: 24px;
  border: 4px solid #fff;
  border-color: #FFFFFF !important;
  background-color: #70D24E !important;
}
</style>

<style scoped src="@/styles/filter-input.css"></style>
<style scoped>
.filter-input {
  width: 235px;
  padding: 0 30px;
}
</style>