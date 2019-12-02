<template>
  <div id="app" class="container">
    <UpcomingEvents/>
  </div>
</template>

<script>
import UpcomingEvents from '@/components/UpcomingEvents'
export default {
  name: 'app',
  components: {
    UpcomingEvents
  }
}
</script>

<style lang="stylus">
@import './smart-grid.styl'
// reset()
*
  box-sizing border-box
body
  background-color #252C3C
.containter
  wrapper-full() 
  padding 30px

#app
  max-width 350px
  font-family 'Avenir', Helvetica, Arial, sans-serif
  color #2c3e50
</style>
