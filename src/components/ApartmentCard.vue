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
    return {
    }
  }
}
</script>
<style scoped>

.button {
  font-weight: bold;
  text-transform: uppercase;
  line-height: 28px;
}

.button_main {
  display: none;
  text-decoration: none;
  transform: translateY(40px);
  margin-top: 10px;
  text-align: center;
  font-size: 14px;
  padding: 5px 54px;
  background-color: #70D24E;
  border-radius: 5px;
  color: #fff;
  border-radius: 2px 2px 5px 5px;
}


.apartment-card {
  overflow: hidden;
  transition: .3s;
  width: 270px;
  height: 365px;
  display: flex;
  flex-direction: column;
  background: #FFFFFF;
  box-shadow: 0px 5px 20px rgba(86, 86, 86, 0.05);
  border-radius: 10px;
  padding: 0 10px;
  padding-top: 12px;
  padding-bottom: 10px;
}

.apartment-card:focus,
.apartment-card:focus-within,
.apartment-card:hover {
  box-shadow: 0px 5px 20px rgba(86, 86, 86, 0.25);
}

.apartment-card:focus .apartment-card__image img,
.apartment-card:focus-within .apartment-card__image img,
.apartment-card:hover .apartment-card__image img {
  max-height: 152px;
  width: auto;
}

.apartment-card:hover .button_main,
.apartment-card:focus .button_main,
.apartment-card:focus-within  .button_main {
  display: block;
  transition: .3s;
  transform: translateY(0);
}

.apartment-card__header {
  display: flex;
  justify-content: space-between;
}

.apartment-card__image-container {
  height: auto;
  position: relative;
  background-color: #FFFFFF;
  border: 1px solid #EBEBEB;
  box-sizing: border-box;
  border-radius: 5px;
  flex-shrink: 2;
}

.apartment-card__image-header {
  display: flex;
  justify-content: flex-end;
}
.apartment-card__image-label {
  height: 30px;
  padding: 0 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #FFFFFF;
  border-left: 1px solid #EBEBEB;
  border-bottom: 1px solid #EBEBEB;
  box-sizing: border-box;
  border-radius: 0px 5px;

  font-weight: bold;
  font-size: 14px;
  line-height: 28px;


  text-transform: uppercase;

  /* Black */

  color: #2C323A;

}

.apartment-card__image {
  height: auto;
  /* padding: 0 10px; */
  padding-bottom: 30px;
  display: flex;
  text-align: center;
  justify-content: center;
}


.apartment-card:hover .apartment-card__image,
.apartment-card:focus .apartment-card__image,
.apartment-card:focus-within .apartment-card__image {
  padding-bottom: 25px;
}


.apartment-card__image img {
  max-width: 230px;
  max-height: 188px;
  width: auto;
  transition: 0.3s;
}

.apartment-card__header-item {
  display: flex;
}

.apartment-card__header-item__separator {
  display: flex;
  align-items: center;
  font-size: 12px;
  margin: 0 10px;
}

.apartment-card__text {
  font-weight: bold;
  font-size: 12px;
  line-height: 28px;
  color: #2C323A;
}

.apartment-card__text_secondary {
  opacity: 0.5;
}

.apartment-card:hover .apartment-card__title_secondary,
.apartment-card:focus .apartment-card__title_secondary,
.apartment-card:focus-within .apartment-card__title_secondary {
  line-height: 18px;
}


.apartment-card__footer {
  margin-top: 10px;
  flex-grow: 2; 
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.apartment-card__title {
  text-align: right;
  font-weight: bold;
  font-size: 20px;
  line-height: 28px;
  /* Black */

  color: #2C323A;
}

.apartment-card__title_secondary {
  opacity: .5;
  font-size: 12px;
  line-height: 28px;
}


</style>