<template>
  <div id="app">
    <Navbar v-if="!isCFP" />
    <transition :name="transitionName">
      <keep-alive>
        <router-view class="main-view" />
      </keep-alive>
    </transition>
  </div>
</template>

<script>
import * as Layout from '@/components'
export default {
  components: {
    ...Layout
  },
  data () {
    return {
      isCFP: false,
      transitionName: 'slide-left'
    }
  },
  mounted () {
    this.toggleNavbar()
  },
  methods: {
    toggleNavbar () {
      if (this.$route.name === 'CFP') this.isCFP = true
      else this.isCFP = false
    }
  },
  watch: {
    $route (to, from) {
      this.toggleNavbar()
      const toDepth = to.meta.index
      const fromDepth = from.meta.index
      this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
    }
  }
}
</script>

<style lang="scss">
@import './assets/scss/main.scss';

.main-view {
  min-height: 100vh;
  transition-property: transform,opacity;
  transition-duration: .5s;
  transition-timing-function: cubic-bezier(.55, 0, .1, 1);
}
</style>
