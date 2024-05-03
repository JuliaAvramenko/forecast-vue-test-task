<script setup>
import Widget from './components/Widget.vue'

</script>

<template>
  <div class="page">
      <main class="main">
        <div class="container">
          <div class="laptop">
            <Widget />         
           
          </div>
        </div>
      </main>
    </div>
</template>

<style lang="sass" scoped>
@import './assets/styles/main'

.page
  position: relative
  display: flex
  justify-content: center
  align-items: center
  min-height: 100vh
  padding: 20px 0
  background-color: #59585d

.container
  max-width: 1200px
  min-width: 400px
  width: 100%
  margin: 0 auto
  padding: 0 3%

.laptop
  width: 100%
  padding: 20px
  background-color: #0e100f
  border-radius: 25px

</style>
