<template>
  <div class="apartment-card"
    aria-label="Квартира"
    tabindex="0">
    <div class="apartment-card__header">
      <div class="apartment-card__header-item">
        <div class="apartment-card__text apartment-card__text_secondary">{{data.floor}} этаж</div>
      </div>
      <div class="apartment-card__header-item">
        <div class="apartment-card__text">{{data.rooms}} комната</div>
        <div class="apartment-card__header-item__separator">-</div>
        <div class="apartment-card__text">{{data.square}}м<sup>2</sup></div>
      </div>
    </div>
    <div class="apartment-card__image-container">
      <div class="apartment-card__image-header">
        <div class="apartment-card__image-label">№{{data.id}}</div>
      </div>
      <div class="apartment-card__image">
        <img src="@/assets/images/image.jpg" alt="Схема квартиры">
      </div>
    </div>
    <div class="apartment-card__footer">
      <div class="apartment-card__title">{{data.price.toLocaleString('ru')}}р.</div>
      <div class="apartment-card__title apartment-card__title_secondary">{{Math.floor(data.price / data.square).toLocaleString('ru')}}р. за м<sup>2</sup></div>
      <a href="#" @mouseup="$event.target.blur()" tabindex="0" class="button button_main">Подробнее</a>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ApartmentCard',
  props: ['data', 'button'],
  data() {
    return {}
  }
}
</script>
<style scoped src="@/styles/apartment-card.css"></style>
<style scoped>

.button_main {
  display: none;
  transform: translateY(40px);
  margin-top: 10px;
  color: #fff;
  border-radius: 2px 2px 5px 5px;
}

</style>