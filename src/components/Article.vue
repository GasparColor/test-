<template lang="pug">
  .article
    header.article__header
      img.article__headerImg(:src="require(`../assets/group-5.png`)")

    main.article__main
      h2.article__title(v-text="$props.view.title")
      p.article__text(v-text="$props.view.text")

      dl.article__totalList.totalList
        .totalList__item(
          v-for="(item, index) in $props.view.totalList"
          :key="index"
        )
          dt.totalList__key(v-text="item.key")
          dd.totalList__value(v-text="item.value")

      ul.article__operations.operations
        li.operations__item(
          v-for="(item, index) in $props.view.operations"
          :key="index"
        )
          time.operations__date(
            v-if="item.date"
            v-text="item.date"
          )

          .operations__imgWrapper(:class="iconLineClass[index]")
            .operations__img(
              v-if="item.icon"
              :class="item.icon"
            )
              img(:src="require(`../assets/${item.icon}.svg`)")

          .operations__textWrapper
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
              :class="button.type"
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
    matchIconLineClass() {
      this.$props.view.operations.forEach((val, key) => {
        if (this.$props.view.operations[key + 1]) {
          this.iconLineClass.push(this.$props.view.operations[key].icon
            + this.$props.view.operations[key + 1].icon);
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

$breakpoints: (
  phone: 640px,
  tablet: 768px,
  desktop: 1024px);


.article {
  display: flex;
  flex-direction: column;
}

.article__header {
  max-width: 1440px;
  margin: 0 auto;
  /*margin-top: -30px;*/
}

.article__headerImg {
  width: 100%;
}

.article__title {
  max-width: 58%;
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
  max-width: 58%;
  margin: 0 auto;
  padding: 0 20px;
  font-size: 32px;
  line-height: 1.25;
  color: #000000;
}

@include media("<tablet") {
  .article__text {
    max-width: 100%;
    font-size: 20px;
    line-height: 1.3;
  }
}

.article__totalList {
  max-width: 58%;
  margin: 54px auto 24px;
  padding: 0 20px;
}

@include media("<tablet") {
  .article__totalList {
    max-width: 100%;
    margin: 30px auto 24px;
  }
}

.totalList__key{
  position: relative;
  float: left;
  margin-right: 15px;
  &::after{
    position: absolute;
    right: -8px;
    content: ':'
  }
}

.totalList__value {
  margin-left: 0;
}

.totalList__key,
.totalList__value {
  font-size: 20px;
  line-height: 1.4;
  color: #7c8a9c;
}

@include media("<tablet") {
  .totalList__key,
  .totalList__value {
    font-size: 15px;
    line-height: normal;
  }
}

.totalList__item:first-child {
  .totalList__key,
  .totalList__value {
    font-size: 32px;
    font-family: "Bnpp-rounded-bold", Helvetica, Arial, sans-serif;
    line-height: 1.25;
    color: #000000;
  }
}

@include media("<tablet") {
  .totalList__item {
    margin-bottom: 3px;
    &:first-child {
      margin-bottom: 4px;
      .totalList__key,
      .totalList__value {
        font-size: 20px;
        line-height: 1.3;
      }
    }
  }
}

.operations {
  max-width: 58%;
  margin: 0 auto;
  padding: 0 20px;
  list-style: none;
}

@include media("<tablet") {
  .operations {
    max-width: 100%;
  }
}

.operations__item {
  position: relative;
  &:last-child .operations__img::before {
    display: none
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

.operations__textWrapper {
  position: relative;
}

.operations__imgWrapper {
  position: absolute;
  top: 15px;
  left: -66px;
  height: 100%;
}

@include media("<tablet") {
  .operations__imgWrapper {
    left: -49px;
  }
}

.operations__text {
  margin: 4px 0 30px;
  font-size: 28px;
  line-height: 1.21;
  color: #000000;
}

@include media("<tablet") {
  .operations__text {
    font-size: 20px;
    line-height: 1.3;
  }
}

.operations__img {
  display: flex;
  top: -3px;
  left: -62px;
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

    &.cart {
      background-color: #f0f0f3;
    }

    &.injury {
      background-color: #f05454;
    }

    &.call {
      background-color: #feb800;
    }

    &.doc {
      background-color: #7d899c;
    }

    &.money {
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

@include media("<tablet") {
  .operations__decrement,
  .operations__increment {
    font-size: 15px;
    line-height: normal;
    right: 0;
    top: -14px;
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
  max-width: 58%;
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
    text-align:center;
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

@include media("<tablet") {
  .assessment__list {
    justify-content: center;
  }
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

  &.good {
    color: #249d6d;
    background: url("../assets/good.svg") no-repeat center 25%;
  }

  &.normal {
    color: #7c8a9c;
    background: url("../assets/normal.svg") no-repeat center 25%;
  }

  &.bad {
    color: #bb1f70;
    background: url("../assets/bad.svg") no-repeat center 25%;
  }
}

@include media("<tablet") {
  .assessment__button {
    font-size: 16px;
    line-height: 1.5;
    width: 112px;
  }
}


/*CART*/
.operations__imgWrapper.cartcart .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #f0f0f3);
}
.operations__imgWrapper.cartinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #f05454);
}
.operations__imgWrapper.cartcall .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #feb800);
}
.operations__imgWrapper.cartdoc .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #7d899c);
}
.operations__imgWrapper.cartmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #159e6f);
}

/*INJURY*/
.operations__imgWrapper.injuryinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #f05454);
}
.operations__imgWrapper.injurycart .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #f0f0f3);
}
.operations__imgWrapper.injurycall .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #feb800);
}
.operations__imgWrapper.injurydoc .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #7d899c);
}
.operations__imgWrapper.injurymoney .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #159e6f);
}

/*CALL*/
.operations__imgWrapper.callcall .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #feb800);
}
.operations__imgWrapper.callcart .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #f0f0f3);
}
.operations__imgWrapper.callinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #f05454);
}
.operations__imgWrapper.calldoc .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #7d899c);
}
.operations__imgWrapper.callmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #159e6f);
}

/*DOC*/
.operations__imgWrapper.docdoc .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #7d899c);
}
.operations__imgWrapper.doccart .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #f0f0f3);
}
.operations__imgWrapper.docinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #f05454);
}
.operations__imgWrapper.doccall .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #feb800);
}
.operations__imgWrapper.docmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #159e6f);
}

/*MONEY*/
.operations__imgWrapper.moneymoney .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #159e6f);
}
.operations__imgWrapper.moneycart .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #f0f0f3);
}
.operations__imgWrapper.moneyinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #f05454);
}
.operations__imgWrapper.moneycall .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #feb800);
}
.operations__imgWrapper.moneydoc .operations__img::before{
  background-image: linear-gradient(to bottom, #159e6f, #7d899c);
}
</style>
