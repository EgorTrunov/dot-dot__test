<template>
<!-- eslint-disable max-len -->
  <main>
  <h1 class="title">FTL: Прямая машина</h1>
  <div class="container">
    <form class="forms">
      <fieldset class="forms__items forms__items--route">
        <legend class="forms__title"><span>1</span>Маршрут</legend>
        <label class="forms__label">
          <span>Откуда</span>
          <input class="forms__input" type="text">
        </label>
        <label class="forms__label" for="">
          <span>Куда</span>
          <input class="forms__input" type="text">
        </label>
      </fieldset>
      <fieldset class="forms__items forms__items--transport">
        <legend class="forms__title"><span>2</span>Транспорт</legend>
          <label class="forms__label">
            <span>Грузоподъёмность</span>
            <div class="forms__select" name="select" @click="carrying = !carrying" key="carrying">
              <p class="forms__select--active">{{ carryingValue }}</p>
              <div class="select__inner">
              <ul class="select__list" v-if="carrying">
                <li class="select__item" v-for="(item, index) in items" :key="index" @click="selectItem(index, 'carryingValue')">{{ item }}</li>
              </ul>
              </div>
              <span class="arrow">
                <img class="img__arrow" src="@/assets/images/arrow.svg" v-if="!carrying">
                <img class="img__arrow" src="@/assets/images/arrow-rotate.svg" v-else>
              </span>
            </div>
          </label>
          <label class="forms__label">
            <span>Способ погрузки</span>
            <div class="forms__select" name="select" @click="shipment = !shipment" key="shipment">
              <p class="forms__select--active">{{ shipmentValue }}</p>
              <div class="select__inner">
              <ul class="select__list" v-if="shipment">
                <li class="select__item" v-for="(item, index) in items" :key="index" @click="selectItem(index, 'shipmentValue')">{{ item }}</li>
              </ul>
              </div>
              <span class="arrow">
                <img class="img__arrow" src="@/assets/images/arrow.svg" v-if="!shipment">
                <img class="img__arrow" src="@/assets/images/arrow-rotate.svg" v-else>
              </span>
            </div>
          </label>
      </fieldset>
      <fieldset class="forms__items forms__items--cargo">
        <legend class="forms__title"><span>3</span>Груз</legend>
        <label class="forms__label">
          <span>Тип груза</span>
            <div class="forms__select" name="select" @click="typeCargo = !typeCargo" key="typeCargo">
              <p class="forms__select--active">{{ typeCargoValue }}</p>
              <div class="select__inner">
              <ul class="select__list" v-if="typeCargo">
                <li class="select__item" v-for="(item, index) in items" :key="index" @click="selectItem(index, 'typeCargoValue')">{{ item }}</li>
              </ul>
              </div>
              <span class="arrow">
                <img class="img__arrow" src="@/assets/images/arrow.svg" v-if="!typeCargo">
                <img class="img__arrow" src="@/assets/images/arrow-rotate.svg" v-else>
              </span>
            </div>
        </label>
        <label class="forms__label">
          <span>Класс опасности</span>
            <div class="forms__select" name="select" @click="danger = !danger" key="danger">
              <p class="forms__select--active">{{ dangerValue }}</p>
              <div class="select__inner">
              <ul class="select__list" v-if="danger">
                <li class="select__item" v-for="(item, index) in items" :key="index" @click="selectItem(index, 'dangerValue')">{{ item }}</li>
              </ul>
              </div>
              <span class="arrow">
                <img class="img__arrow" src="@/assets/images/arrow.svg" v-if="!danger">
                <img class="img__arrow" src="@/assets/images/arrow-rotate.svg" v-else>
              </span>
            </div>
        </label>
        <label class="forms__label">
          <span>Объявленная ценность, &#8381;</span>
          <input class="forms__input" type="text" placeholder="&ge; 0">
        </label>
        <div class="checkbox__inner">
          <label class="forms__label" for="checkbox">
            <input class="forms__checkbox" id="checkbox" type="checkbox" @click="temp = !temp">
            <span class="forms__checkbox-style"></span>
            <span>Требуется температурный режим</span>
          </label>
        </div>
      </fieldset>
      <fieldset class="forms__items forms__items--temperature" v-if="temp">
        <label class="forms__label">
          <span>От, &#176;C</span>
          <input class="forms__input" type="text" pattern="[0-9]">
        </label>
         <label class="forms__label">
          <span>До, &#176;C</span>
          <input class="forms__input" type="text" pattern="[0-9]">
        </label>
      </fieldset>
      <fieldset class="forms__items forms__items-time">
        <legend class="forms__title"><span>4</span>Время</legend>
        <label class="forms__label">
          Когда прибыл на точку <span>700 км в день</span>
          <div class="time__mark">
            <img class="mark__img" src="@/assets/images/main-dot-red.svg">
            <p class="mark__text">Длинный адрес с градиентом</p>
            <button class="time__btn" type="button">НЕ ВЫБРАНО</button>
          </div>
          <div class="time__mark">
            <img class="mark__img" src="@/assets/images/main-dot-white.svg">
            <p class="mark__text">Адрес не указан</p>
            <button class="time__btn" disabled type="button">НЕ ВЫБРАНО</button>
          </div>
        </label>
      </fieldset>
      <label class="forms__label">
        <span>Комментарий к заказу</span>
      <textarea class="forms__area" placeholder="Укажите особенности въезда на территорию склада или подъезда к адресу"></textarea>
      </label>
    </form>
    <div class="explaining">
      <p class="explaining__text">
        Для расчета стоимости необходимо ввести параметры груза, пункты отправки и прибытия.
      </p>
    </div>
  </div>
  </main>
</template>

<script>
export default {
  name: 'Forms',
  data() {
    return {
      items: [
        'Вариант 1', 'Варинат 2', 'Варинат 3', 'Варинат 4', 'Варинат 5',
      ],
      temp: false,
      carrying: false,
      shipment: false,
      typeCargo: false,
      danger: false,
      carryingValue: 'Не выбрана',
      shipmentValue: 'Не выбрана',
      typeCargoValue: 'Не выбрана',
      dangerValue: 'Не выбрана',
    };
  },
  methods: {
    selectItem(id, value) {
      switch (value) {
        case 'carryingValue':
          this.carryingValue = this.items[id];
          break;
        case 'shipmentValue':
          this.shipmentValue = this.items[id];
          break;
        case 'typeCargoValue':
          this.typeCargoValue = this.items[id];
          break;
        case 'dangerValue':
          this.dangerValue = this.items[id];
          break;
        default:
          break;
      }
    },
  },
};
</script>

<style scoped lang="scss">

// color
$bg-block-color: #4B4B4F;
$default-color: #000000;
$text-color: #FFFFFF;
$decor-color: #EF483E;
$placeholder-color: #CFCFCF;
$noactive-color: #d1d1ec;
$btn-color: #717174;

//font-size
$fz-big: 24px;
$fz-medium: 15px;
$fz-small: 13px;

//width size
$w-100: 100%;
$w-50: 50%;
$w-25: 25%;

// line-heigh
$lh-16: 16px;
$lh-18: 18px;
$lh-19: 19px;
$lh-30: 30px;

%style-input {
  display: block;
  height: 44px;
  border: none;
  margin-top: 8px;
  padding-left: 10px;
  font-size: $fz-medium;
  line-height: $lh-19;
  color: $default-color;
  white-space: nowrap;
  overflow: hidden;
}

%style-select {
  height: 44px;
  border: none;
  margin-top: 8px;
  padding-left: 10px;
  font-size: $fz-medium;
  $lh-18: 18px;
  background-color: $text-color;
  color: $default-color;
}

%style-palceholder {
  font-size: $fz-medium;
  line-height: $lh-19;
  color: $placeholder-color;
}

%gradient {
  white-space: nowrap;
  overflow: hidden;
  position: relative;
}

%gradient--after {
  content: '';
  position: absolute;
  right: 0;
  top: 0;
  width: 35px;
  height: 100%;
  background: linear-gradient(to right, transparent, $text-color 80%);
}
main {
  color: $text-color;
  max-width: 1120px;
  margin: 0 auto;
  padding: 10px;
}

h1 {
  font: {
    weight: bold;
    size: 56px;
  }
  margin-bottom: 20px;
}

.container {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 16px;
}

.forms__items {
  border: none;
}

.forms__title {
  display: flex;
  align-items: center;
  font: {
    size: $fz-big;
    weight: 700;
  }
  line-height: $lh-30;
  margin-bottom: 16px;
  span {
    padding: 1px 7px 2px;
    margin-right: 8px;
    font-size: 16px;
    line-height: 20px;
    background: $decor-color;
    border-radius: 50px;
    text-align: center;
  }
}

.forms__label {
  span {
  font-size: $fz-small;
  line-height: $lh-16;
  }
  font-size: $fz-medium;
  line-height: $lh-18;
  display: block;
  margin-bottom: 16px;
}

.forms__select {
  @extend %style-select;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  cursor: pointer;
  padding: 0 14px;
  .forms__select--active {
    width: 120px;
    @extend %gradient;
  }
  .forms__select--active::after {
    @extend %gradient--after;
  }
  .select__inner {
    position: absolute;
    width: $w-100;
    top: 42px;
    left: 0;
    z-index: 2;
    background: $text-color;
    color: $default-color;
    .select__list {
      list-style: none;
    }
    .select__item {
      padding-left: 12px;
      padding-top: 5px;
      height: 28px;
    }
    .select__item:hover {
      background-color: $decor-color;
      color: $text-color;
      transition: 0.8s;
    }
  }
  .arrow {
    padding: 10px 0 8px 8px;
  }
}

.forms__input::placeholder {
  @extend %style-palceholder;
}

.forms__area {
  @extend %style-input;
  width: $w-100;
  height: 80px;
  resize: none;
  padding: 13px 23px 13px 14px;
  overflow: hidden;
  white-space: pre-wrap;
}

.forms__area::placeholder {
  @extend %style-palceholder;
}

.forms__items--route {
  .forms__input {
    @extend %style-input;
    width: $w-100;
  }
}

.forms__items--transport {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 12px;
  max-width: 356px;
  .forms__select {
    width: $w-100;
  }
}

.forms__items--cargo {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 12px;
  align-items: center;
  max-width: 356px;
  .forms__select {
    @extend %style-select;
    width: $w-100;
  }
  .forms__input {
    @extend %style-input;
    width: $w-100;
  }
  .forms__label:first-of-type {
    grid-column: span 2;
    .forms__select {
      width: $w-100;
    }
    .forms__select--active {
      width: 290px;
    }
  }
  .checkbox__inner {
    width: $w-100;
    grid-column: span 2;
    .forms__label {
    display: flex;
    align-items: center;
    cursor: pointer;
      span {
        margin-left: 36px;
      }
      .forms__checkbox {
        position: absolute;
        z-index: -1;
        opacity: 0;
      }
      .forms__checkbox-style {
        margin: 0;
        width: 24px;
        height: 24px;
        border: 2px solid #C4C4C4;
        border-radius: 2px;
        position: absolute;
      }
      .forms__checkbox:checked+.forms__checkbox-style::before {
        content: '\2713';
        color: $text-color;
        text-align: center;
        padding: 3px;
        position: absolute;
        width: 24px;
        height: 24px;
        background-color: $decor-color;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }
  }
}

.forms__items--temperature {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 16px;
  max-width: 356px;
  .forms__input {
    @extend %style-input;
    width: $w-100;
  }
}

.forms__items-time {
  .forms__label {
    width: $w-100;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    font-size: $fz-small;
    line-height: $lh-16;
  }
  .time__mark {
    display: flex;
    align-items: center;
    justify-content: space-between;
    @extend %style-input;
    background-color: $bg-block-color;
    padding: 10px 10px 10px 8px;
    width: $w-100;
  }
  .mark__img {
    padding: 4px;
  }
  .mark__text {
    background-color: transparent;
    margin-left: 4px;
    border: none;
    padding: 5px 5px;
    color: $placeholder-color;
    margin-right: auto;
    width: 75%;
    @extend %gradient;
  }
  .mark__text::after {
    @extend %gradient--after;
    background: linear-gradient(to right, transparent, $bg-block-color 80%);
  }
  .time__btn {
    padding: 4px 14px 4px 13px;
    background-color: $btn-color;
    border: none;
    border-radius: 2px;
    color: $text-color;
    cursor: pointer;
  }
  .time__btn:disabled {
    opacity: 0.3;
  }
}

.explaining {
  .explaining__text {
    padding: 24px;
    background-color: $bg-block-color;
    font-size: $fz-medium;
    line-height: $lh-18;
  }
}

@media (max-width: 750px) {
  .title {
    font-size: 32px;
  }
  .container {
    grid-template-columns: 1fr;
  }
  .forms__title {
    font-size: 20px;
    line-height: 24px;
  }
  .mark__text {
    max-width: 400px;
  }
}

@media (max-width: 550px) {
  .mark__text {
    max-width: 220px;
  }
}

@media (max-width: 410px) {
.forms,
.explaining {
    max-width: 350px;
  }
  .mark__text {
    max-width: 180px;
  }
}
</style>
