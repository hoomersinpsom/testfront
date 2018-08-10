<template>
  <div>
    <header-bar />
    <profile />
    <bread-crumb :active="1" />
    <personal-data />
  </div>
</template>

<script>
import HeaderBar from '@/components/HeaderBar.vue'
import Profile from '@/components/Profile.vue'
import BreadCrumb from '@/components/BreadCrumb.vue'
import PersonalData from '@/components/PersonalData.vue'

export default {
  name: 'app',
  components: {
    HeaderBar,
    Profile,
    BreadCrumb,
    PersonalData
  }
}
</script>

<style lang="scss">
@import '~@/scss/base';
</style>
