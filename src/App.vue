<template>
  <div id="app">
     <div class="wrapper">
        <header>
           <div class="header__logo"></div>
           <div class="header__phone">8 800 55-00-001</div>
        </header>
     </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  }
}
</script>

<style lang="scss">
@import 'node_modules/bootstrap/scss/bootstrap.scss';
@import 'node_modules/bootstrap-vue/src/index.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.wrapper {
   max-width: 1070px;
   margin: 0 auto;
   border: 1px solid red;
}

header {
   height: 70px;
   display: flex;
   align-items: center;
   justify-content: space-between;

   .header__logo {
      max-height: 32px;
      max-width: 181px;
      width: 100%;
      height: 100%;
      background: url('./assets/svg/mf_logo_full.svg') center / contain no-repeat;
   }

   .header__phone {

   }
}

</style>
