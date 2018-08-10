<template>
  <div class="bread">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-auto">
          <p
            v-for="(step, i) in steps"
            :key="i"
            :class="['item', {'off': i < active, 'active': i === active}]">
            <span class="num">
              <span>{{ i + 1 }}</span>
            </span>
            <span class="text">{{ step }}</span>
          </p>
        </div>
      </div>
    </div>
    <span class="bluebar" :style="{'width': barWidth}"></span>
  </div>
</template>

<script>
export default {
  name: 'BreadCrumb',
  props: {
    active: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      steps: [
        'Simule',
        'Preencha o cadastro',
        'Revise seu pedido',
        'Finalize o pedido'
      ]
    }
  },
  computed: {
    barWidth() {
      return ~~((this.active / this.steps.length) * 100) + '%'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~@/scss/variables';
@import '~@/scss/mixins';
.bluebar{
  display: none;
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  background-color: $blue;
  @include small-device{
    display: block;
  }
  &::after{
    content: '';
    display: block;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 100%;
    border-top: 8px solid transparent;
    border-bottom: 8px solid transparent;
    border-left: 8px solid $blue;
  }
}
.bread{
  background-color: $bone;
  padding: 8px 0;
  position: relative;
  z-index: 0;
  .container{
    @include small-device{
      display: none;
    }
  }
}
.item{
  font-size: 13px;
  text-transform: uppercase;
  margin: 0;
  color: $ash;
  font-weight: 900;
  margin-right: 50px;
  display: inline;
  vertical-align: middle;
  &:last-child{
    margin-right: 0;
  }
  .text{
    display: inline-block;
    vertical-align: middle;
  }
  .num{
    font: 28px;
    height: 28px;
    width: 28px;
    position: relative;
    z-index: 0;
    border-radius: 100%;
    border: 3px solid $ash;
    display: inline-block;
    vertical-align: middle;
    margin-right: 10px;
    span{
      display: block;
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }
  }
  &.active{
    color: $chocodark;
    .num{
      color: $blue;
      border-color: $chocodark;
      background-color: $chocodark;
    }
  }
  &.off{
    .num{
      background-color: $ash;
      color: $bone;
    }
  }
}
</style>
