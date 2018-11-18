<template lang="pug">
  .article
    header.article__header
      img.article__header-img(:src="require(`../assets/header.png`)")

    main.article__main
      h2.article__title(v-text="$props.view.title")
      p.article__text(v-text="$props.view.text")

      dl.article__total-list.total-list
        .total-list__item(
          v-for="(item, index) in $props.view.totalList"
          :key="index"
        )
          dt.total-list__key(v-text="item.key")
          dd.total-list__value(v-text="item.value")

      ul.article__operations.operations
        li.operations__item(
          v-for="(item, index) in $props.view.operations"
          :class="item.date ? 'operations__item--has-date' : ''"
          :key="index"
        )
          time.operations__date(
            v-if="item.date"
            v-text="item.date"
          )

          .operations__img-wrapper(:class="'operations__img-wrapper--' + iconLineClass[index]")
            .operations__img(
              v-if="item.icon"
              :class="'operations__img--' + item.icon"
            )
              img(:src="require(`../assets/${item.icon}.svg`)")

          .operations__text-wrapper
            p.operations__text(v-html="item.text")
            span.operations__decrement(
              v-if="item.decrement"
              v-text="'- ' + item.decrement + ' руб.'"
            )
            span.operations__increment(
            v-if="item.increment"
            v-text="'+ ' + item.increment + ' руб.'"
            )

      .article__footer.assessment
        p.assessment__title(v-text="$props.view.assessment.title")

        ul.assessment__list
          li.assessment__item(
            v-for="(button, index) in $props.view.assessment.buttons"
            :key="index"
            )
            button.assessment__button(
              type="button"
              v-text="button.text"
              :class="'assessment__button--' + button.type"
              @click="buttonHandler(button)"
            )

</template>

<script>
export default {
  name: 'Article',

  data() {
    return {
      iconLineClass: [],
    };
  },

  props: {
    view: {
      type: Object,
      required: true,
    },
  },

  mounted() {
    this.matchIconLineClass();
  },

  methods: {
    // Из названий иконок текущей и следующей акции формируем строку,
    // которую используем как модификатор, по которому задаем цвет полосы,
    // соединяющей две иконки.
    matchIconLineClass() {
      this.$props.view.operations.forEach((val, key) => {
        const currentOperation = this.$props.view.operations[key];
        const nextOperation = this.$props.view.operations[key + 1];

        if (nextOperation) {
          this.iconLineClass.push(currentOperation.icon + nextOperation.icon);
        }
      });
    },

    buttonHandler(button) {
      this.$emit('assessment-button-click', button);
    },
  },
};
</script>

<style scoped lang="scss">
@import "../styles/include-media";

$breakpoints: (tablet: 768px) !default;

.article {
  display: flex;
  flex-direction: column;
}

.article__header {
  max-width: 1440px;
  margin: 0 auto;
}

.article__header-img {
  width: 100%;
}

.article__title {
  max-width: 864px;
  padding: 0 20px;
  margin: 100px auto 24px;
  font-family: "Bnpp-rounded-bold", Helvetica, Arial, sans-serif;
  font-size: 48px;
  line-height: 1.13;
  color: #000000;
}

@include media("<tablet") {
  .article__title {
    max-width: 100%;
    margin: 50px auto 16px;
    font-size: 32px;
    line-height: 1.19;
  }
}

.article__text {
  max-width: 864px;
  margin: 0 auto;
  padding: 0 20px;
  font-size: 32px;
  line-height: 1.25;
  color: #000000;
}

@include media("<tablet") {
  .article__text {
    max-width: 100%;
    padding-right: 32px;
    font-size: 20px;
    line-height: 1.3;
  }
}

.article__total-list {
  max-width: 864px;
  margin: 54px auto 28px;
  padding: 0 20px;
}

@include media("<tablet") {
  .article__total-list {
    max-width: 100%;
    margin: 30px auto 27px;
  }
}

.total-list__key{
  position: relative;
  float: left;
  margin-right: 15px;
  &::after{
    position: absolute;
    right: -8px;
    content: ':'
  }
}

.total-list__value {
  margin-left: 0;
}

.total-list__key,
.total-list__value {
  font-size: 20px;
  line-height: 1.4;
  color: #7c8a9c;
}

@include media("<tablet") {
  .total-list__key,
  .total-list__value {
    font-size: 15px;
    line-height: normal;
  }
}

.total-list__item:first-child {
  .total-list__key,
  .total-list__value {
    font-size: 32px;
    font-family: "Bnpp-rounded-bold", Helvetica, Arial, sans-serif;
    line-height: 1.25;
    color: #000000;
  }
}

@include media("<tablet") {
  .total-list__item {
    margin-bottom: 3px;
    &:first-child {
      margin-bottom: 10px;
      .total-list__key,
      .total-list__value {
        font-size: 20px;
        line-height: 1.3;
      }
    }
  }
}

.operations {
  max-width: 864px;
  margin: 0 auto;
  padding: 0 20px 35px;
  list-style: none;
}

@include media("<tablet") {
  .operations {
    max-width: 100%;
    padding-right: 32px;
    padding-bottom: 17px;
  }
}

.operations__item {
  position: relative;
  &:last-child .operations__img::before {
    display: none
  }
  &:not(.operations__item--has-date) {
    margin-top: -6px;
  }
}

@include media('>=tablet', '<980px') {
  .operations__item {
    margin-left:69px;

  & :not(.operations__item--has-date) .operations__text {
      margin-top: 6px;
    }
  }
}

@include media("<tablet") {
  .operations__item {
    margin-left: 50px;
  }
}

.operations__date {
  font-size: 20px;
  line-height: 1.4;
  color: #7c8a9c;
}

@include media("<tablet") {
  .operations__date {
    font-size: 15px;
    line-height: normal;
  }
}

.operations__text-wrapper {
  position: relative;
}

.operations__text {
  margin: 5px 0 30px;
  font-size: 28px;
  line-height: 1.21;
  color: #000000;
}

@include media("<tablet") {
  .operations__text {
    margin-bottom: 19px;
    margin-top: 4px;
    font-size: 20px;
    line-height: 1.3;
  }

  .operations__item:not(.operations__item--has-date) .operations__text {
    margin-top: 25px;
  }
}

.operations__img-wrapper {
  position: absolute;
  top: -4px;
  left: -61px;
  height: 98%;
}

.operations__item--has-date {
  .operations__img-wrapper {
    top: 27px;
  }
  + .operations__item:not(.operations__item--has-date) .operations__img-wrapper {
    height: 120%;
  }
}

@include media("<tablet") {
  .operations__item:not(.operations__item--has-date) .operations__img-wrapper {
    top: -5px !important;
  }
}

@include media("<tablet") {
  .operations__img-wrapper {
    left: -49px;
    top: 15px !important;
  }
}

.operations__img {
  display: flex;
  width: 34px;
  height: 34px;
  z-index: 99;
  outline: 4px solid #ffffff;
  background-color: #f0f0f3;
  border-radius: 50px;

  &::before {
      position: absolute;
      content: '';
      bottom: -33px;
      z-index: -9;
      right: 50%;
      width: 4px;
      height: 100%;
      background-image: linear-gradient(to bottom, #f0f0f3, #f05454);
  }

  img {
    margin: auto;
    position:relative;
  }

  &.operations__img--cart {
    background-color: #f0f0f3;
  }

  &.operations__img--injury {
    background-color: #f05454;
  }

  &.operations__img--call {
    background-color: #feb800;
  }

  &.operations__img--doc {
    background-color: #7d899c;
  }

  &.operations__img--money {
    background-color: #159e6f;
  }
}

.operations__decrement,
.operations__increment {
  position: absolute;
  right: -133px;
  top: 2px;
  font-size: 20px;
  line-height: 1.4;
}

@include media("<1135px") {
  .operations__decrement,
  .operations__increment {
    right: 0;
    top: -20px;
  }
}

@include media("<tablet") {
  .operations__decrement,
  .operations__increment {
    font-size: 15px;
    line-height: normal;
  }
  .operations__item:not(.operations__item--has-date) {
    .operations__decrement,
    .operations__increment {
      top: -13px;
    }
  }
}

.operations__decrement {
  color: #f05454;
}

.operations__increment {
  color: #159e6f;
}

.assessment {
  margin: 0 auto;
  max-width: 864px;
  border-top: 1px solid #e5e5ea;
  padding:0 20px 100px;
}

@include media("<tablet") {
  .assessment {
    max-width: 100%;
  }
}

.assessment__title {
  margin: 24px 0 16px;
  font-size: 19px;
  line-height: normal;
  color: #7c8a9c;
}

@include media("<tablet") {
  .assessment__title {
    margin-bottom: 14px;
    text-align:left;
    font-size: 16px;
    line-height: 1.25;
  }
}

.assessment__list {
  display: flex;
  margin: 0 auto;
  padding: 0;
  list-style: none;
}

.assessment__button {
  border: none;
  font-size: 19px;
  line-height: normal;
  outline: 1px solid #e5e5ea;
  border-radius: 5px;
  height: 69px;
  padding: 32px  0 0;
  width: 160px;

  &:hover:not(:disabled){
    cursor: pointer;
    outline: 1px solid #9e9e9e;
  }

  &.assessment__button--good {
    color: #249d6d;
    background: url("../assets/good.svg") no-repeat center 25%;
  }

  &.assessment__button--normal {
    color: #7c8a9c;
    background: url("../assets/normal.svg") no-repeat center 25%;
  }

  &.assessment__button--bad {
    color: #bb1f70;
    background: url("../assets/bad.svg") no-repeat center 25%;
  }
}

@include media("<tablet") {
  .assessment__button {
    font-size: 16px;
    line-height: 1.5;
    width: 111px;
  }
}

/*CART*/
.operations__img-wrapper.operations__img-wrapper--cartcart .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #f0f0f3);
}
.operations__img-wrapper.operations__img-wrapper--cartinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #f05454);
}
.operations__img-wrapper.operations__img-wrapper--cartcall .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #feb800);
}
.operations__img-wrapper.operations__img-wrapper--cartdoc .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #7d899c);
}
.operations__img-wrapper.operations__img-wrapper--cartmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #159e6f);
}

/*INJURY*/
.operations__img-wrapper.operations__img-wrapper--injuryinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #f05454);
}
.operations__img-wrapper.operations__img-wrapper--injurycart .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #f0f0f3);
}
.operations__img-wrapper.operations__img-wrapper--injurycall .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #feb800);
}
.operations__img-wrapper.operations__img-wrapper--injurydoc .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #7d899c);
}
.operations__img-wrapper.operations__img-wrapper--injurymoney .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #159e6f);
}

/*CALL*/
.operations__img-wrapper.operations__img-wrapper--callcall .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #feb800);
}
.operations__img-wrapper.operations__img-wrapper--callcart .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #f0f0f3);
}
.operations__img-wrapper.operations__img-wrapper--callinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #f05454);
}
.operations__img-wrapper.operations__img-wrapper--calldoc .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #7d899c);
}
.operations__img-wrapper.operations__img-wrapper--callmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #159e6f);
}

/*DOC*/
.operations__img-wrapper.operations__img-wrapper--docdoc .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #7d899c);
}
.operations__img-wrapper.operations__img-wrapper--doccart .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #f0f0f3);
}
.operations__img-wrapper.operations__img-wrapper--docinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #f05454);
}
.operations__img-wrapper.operations__img-wrapper--doccall .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #feb800);
}
.operations__img-wrapper.operations__img-wrapper--docmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #159e6f);
}

/*MONEY*/
.operations__img-wrapper.operations__img-wrapper--moneymoney .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #159e6f);
}
.operations__img-wrapper.operations__img-wrapper--moneycart .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #f0f0f3);
}
.operations__img-wrapper.operations__img-wrapper--moneyinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #f05454);
}
.operations__img-wrapper.operations__img-wrapper--moneycall .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #feb800);
}
.operations__img-wrapper.operations__img-wrapper--moneydoc .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #7d899c);
}
</style>
