<template>
  <div class="filter-input" role="group" aria-labelledby="id-group-label">
    <div id="id-group-label" class="filter-input__title">{{ title }}</div>
    <ul class="filter-input__selectors">
      <li v-for="(checkbox, i) in checkboxValues" :key="i">
        <div
          class="filter-input__selectors__item"
          role="checkbox"
          tabindex="0"
          :class='{"filter-input__selectors__item_active": checkbox.active}'
          :aria-checked="checkbox.active.toString()"          
          @click="handleClick($event, checkbox)"
          @keypress="handleKeyPress($event, checkbox)"
          >
            {{checkbox.value}}
          </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: ['values', 'title'],
  data() {
    return {
      checkboxValues: [],
      rangeValues: []
    }
  },
  methods: {
    handleKeyPress(event, checkbox) {
      if(event.code === 'Space') {
        event.preventDefault()
        checkbox.active = !checkbox.active;
        this.inputEmit()
      }
    },
    setDefault() {
      console.log("?")
      this.checkboxValues = this.checkboxValues.map(value => {
        value.active = true
        return value
      })
      this.inputEmit()
    },
    handleClick(event, checkbox) {
      checkbox.active = !checkbox.active;
      this.inputEmit()
      event.target.blur()
    },
    inputEmit() {
      this.$emit('input', this.checkboxValues.filter(e => e.active).map(e => e.value))
    },
    updateValues(newValues) {
      this.checkboxValues = newValues.map(value => {
        return { value, active: true }
      })
    }
  },
  mounted() {
    this.updateValues(this.values)
    this.$nextTick(() => {
      this.inputEmit()
    })
    
  },
  watch: {
    values (newValues) {
      this.updateValues(newValues)
    }
  }
}
</script>
<style scoped src="@/styles/filter-input.css"></style>

