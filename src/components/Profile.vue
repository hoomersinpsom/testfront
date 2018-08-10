<template>
  <div class="profile">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-3 first">
          <p class="title">Me Chamo:</p>
          <p class="text">Paul Irish</p>
          <p class="small">
            <span>CPF:</span>
            762.888.176-92
          </p>
        </div>
        <div class="col-auto ml-auto">
          <p class="title">preciso de:</p>
          <p class="text">R$ 2.000</p>
        </div>
        <div class="col-auto">
          <p class="title">quero pagar em</p>
          <p class="text">12 vezes</p>
        </div>
        <div class="col-auto">
          <p class="title">para:</p>
          <p class="text">COMPRAR UMA BIKE</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import '~@/scss/variables';
@import '~@/scss/mixins';
.ml-auto{
  @include small-device{
    margin-left: 0;
  }
}
@include small-device{
  .first{
    margin-bottom: 20px;
  }
}
.profile{
  background-color: $choco;
  padding: 20px 0;
}
p{
  text-transform: uppercase;
  margin-bottom: 0;
  line-height: 1.2em;
  &.title{
    font-size: 10px;
    color: $blue;
  }
  &.text{
    color: $milk;
    font-size: 23px;
    font-weight: bold;
  }
  &.small{
    font-size: 10px;
    color: $milk;
    span{
      color: $blue;
    }
  }
}
</style>
