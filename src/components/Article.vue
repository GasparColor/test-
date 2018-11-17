<template lang="pug">
  div.article
    header.article__header
      img.article__headerImg(:src="require(`../assets/group-5.png`)")

    main.article__main
      h2.article__title(v-text="$props.view.title")
      p.article__text(v-text="$props.view.text")

      dl.article__totalList.totalList
        div.totalList__item(v-for="(item, index) in $props.view.totalList" :key="index")
          dt.totalList__key(v-text="item.key")
          dd.totalList__value(v-text="item.value")

      ul.article__operations.operations
        li.operations__item(
          v-for="(item, index) in $props.view.operations"
          :key="index"
          )

          time.operations__date(v-if="item.date" v-text="item.date")

          div.operations__imgWrapper(:class="values[index]")
            div.operations__img(v-if="item.icon" :class="item.icon")
              img(:src="require(`../assets/${item.icon}.svg`)")

          div.operations__textWrapper
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
            button.assessment__button(type="button" v-text="button.text" :class="button.type")

</template>

<script>
export default {
  name: 'Article',

  data() {
    return {
      values: [],
    };
  },

  props: {
    view: {
      type: Object,
      required: true,
    },
  },


  mounted() {
    this.$props.view.operations.forEach((val, key) => {
      if (this.$props.view.operations[key + 1]) {
        this.values.push(this.$props.view.operations[key].icon
          + this.$props.view.operations[key + 1].icon);
      }
    });
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
}

.article__headerImg {
  width: 100%;
}

.article__main {
  max-width: 55%;
  margin: 0 auto;
}


.article__title {
  margin: 100px 0 24px;
  font-family: "Bnpp-rounded-bold", Helvetica, Arial, sans-serif;
  font-size: 48px;
  line-height: 1.13;
  color: #000000;
}

@include media("<tablet") {
  .article__title {
    font-size: 32px;
    line-height: 1.19;
  }
}

.article__text {
  margin: 0;
  font-size: 32px;
  line-height: 1.25;
  color: #000000;
}

@include media("<tablet") {
  .article__text {
    font-size: 20px;
    line-height: 1.3;
  }
}

.article__totalList {
  margin: 54px 0 24px;
}

.totalList__item {
  display: flex;
}

.totalList__key{
  position: relative;
  &::after{
    position: absolute;
    right: -8px;
    content: ':'
  }
}

// TODO mixin
.totalList__value {
  margin-left: 14px;
}

.totalList__key,
.totalList__value {
  font-size: 20px;
  line-height: 1.4;
  color: #7c8a9c;
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

.operations {
  margin: 0;
  padding: 0;
  list-style: none;
}
.operations__item {
  position: relative;
}
.operations__item:last-child .operations__img::before {
  display: none;
}

.operations__date {
  font-size: 20px;
  line-height: 1.4;
  color: #7c8a9c;
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

.operations__imgWrapper.cartinjury .operations__img::before{
  background-image: linear-gradient(to bottom, #f0f0f3, #f05454);
}

.operations__imgWrapper.injurycart .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #f0f0f3);
}

.operations__imgWrapper.injurycall .operations__img::before{
  background-image: linear-gradient(to bottom, #f05454, #feb800);
}
.operations__imgWrapper.calldoc .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #7d899c);
}
.operations__imgWrapper.doccall .operations__img::before{
  background-image: linear-gradient(to bottom, #7d899c, #feb800);
}
.operations__imgWrapper.callcall .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #feb800);
}
.operations__imgWrapper.callmoney .operations__img::before{
  background-image: linear-gradient(to bottom, #feb800, #159e6f);
}

.operations__text {
  font-size: 28px;
  line-height: 1.21;
  color: #000000;
  margin: 4px 0 30px;
}

.operations__img {
  top: -3px;
  left: -62px;
  display: flex;
  z-index: 99;
  outline: 4px solid #ffffff;
  width: 34px;
  height: 34px;
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

.operations__decrement {
  color: #f05454;
}

.operations__increment {
  color: #159e6f;
}

.assessment {
  border-top: 1px solid #e5e5ea;
  padding-bottom: 100px;
}

.assessment__title {
  margin: 24px 0 16px;
  font-size: 19px;
  line-height: normal;
  color: #7c8a9c;
}

.assessment__list {
  display: flex;
  margin: 0;
  padding: 0;
  list-style: none;
}

.assessment__button {
  border: none;
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
</style>
