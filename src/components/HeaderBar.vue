<template>
  <header>
    <div class="container-fluid">
      <div class="row align-items-center">
        <div class="col">
          <img src="@/assets/logo.png">
        </div>
        <nav class="col menu">
          <a href="#">como funciona</a>
          <span></span>
          <a href="#">privacidade</a>
          <span></span>
          <a href="#">ajuda</a>
        </nav>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@import '~@/scss/variables';
@import '~@/scss/mixins';

header{
  background-color: $chocodark;
  padding-top: 20px;
  padding-bottom: 20px;
}
.menu{
  text-align: right;
  @include small-device{
    text-align: center;
  }
  a{
    display: inline;
    vertical-align: middle;
    text-transform: uppercase;
    color: $milk;
    font-size: 13px;
    letter-spacing: 1px;
    &:hover{
      color: $blue;
    }
  }
  span{
    display: inline-block;
    vertical-align: middle;
    width: 6px;
    height: 6px;
    border: 1px solid $blue;
    border-radius: 100%;
    margin: 0 15px;
    @include small-device{
      display: block;
      height: 1px;
      width: 100%;
      margin: 0;
    }
  }
}
</style>
