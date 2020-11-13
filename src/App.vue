<template>
   <div id="app">

      <header>
         <div class="wrapper">
            <div class="header__logo"></div>
            <h6 class="header__phone">8 800 55-00-001</h6>
         </div>
      </header>

      <div class="wrapper">
         <div class="big-title">
            <h1>Помощь и обслуживание клиентов</h1>
         </div>
         <!--         <Tabs />-->
         <div class="tabs">
            <div @click="activeTab = !activeTab" class="tabs__tab" :class="{active: activeTab}">
               <svg xmlns="http://www.w3.org/2000/svg" width="29" height="24.379" viewBox="0 0 29 24.379">
                  <defs></defs>
                  <g transform="translate(-1 -3.596)">
                     <path class="a" d="M19.9,20.56,18.43,19,17,20.38,19.45,23h.89l4.44-4.68-1.46-1.38Z"/>
                     <path class="a"
                           d="M28.43,22.61A8.291,8.291,0,0,0,18.7,11.58,8.358,8.358,0,1,0,2,12.33a8.25,8.25,0,0,0,.54,2.94L1,18l2,2.71,3.58-1a8.2,8.2,0,0,0,5.77.68,8.32,8.32,0,0,0,12.1,6.66l3.32.92L30,25.5ZM7.19,17.81l-.29-.17-3.09.78-.49-.65L4.76,15.3l-.18-.41A6.36,6.36,0,1,1,7.2,17.81ZM27,25.7l-2.84-.77-.36.21a6.32,6.32,0,0,1-9.51-5.46,8.35,8.35,0,0,0,4.28-6,6.33,6.33,0,0,1,7.84,8.55l-.18.41,1.17,2.55Z"/>
                     <circle class="a" cx="1.1" cy="1.1" r="1.1" transform="translate(9.27 14.9)"/>
                     <path class="a" d="M10.37,14H9.49V12h.87a1,1,0,1,0-1-1h-2a3,3,0,1,1,3,3Z"/>
                  </g>
               </svg>
               Часто задаваемые вопросы
            </div>
            <div @click="activeTab = !activeTab" class="tabs__tab" :class="{active: !activeTab}">
               <svg xmlns="http://www.w3.org/2000/svg" width="17" height="24" viewBox="0 0 17 24">
                  <defs></defs>
                  <rect class="a" width="7" height="2" transform="translate(4 5)"/>
                  <rect class="a" width="8" height="2" transform="translate(4 9)"/>
                  <rect class="a" width="4" height="2" transform="translate(4 13)"/>
                  <path class="a" d="M17,13V0H0V24H17Zm-2,9H2V2H15V22Zm1.5,0h0"/>
               </svg>
               Инструкции
            </div>
         </div>

         <div v-if="activeTab" class="tab-content">
            <div class="tab-content__questions">
               <h3>Вопросы по темам <span></span></h3>
               <div class="tab-content__collapse">
                  <p v-b-toggle.collapse-1>МегаФон ТВ</p>
                  <b-collapse id="collapse-1">
                     <div class="tab-content__collapse_qustion">
                        – Что такое МегаФон ТВ?
                     </div>
                     <div class="tab-content__collapse_answer">
                        МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами,
                        новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart
                        TV, Android TV, в смартфоне, планшете и браузере
                     </div>
                  </b-collapse>
               </div>

            </div>

         </div>
         <div v-if="!activeTab" class="tab-content">
            <div class="tab-content__directions">Вопросы2</div>
         </div>
      </div>
   </div>
</template>

<script>
// import Tabs from "@/components/Tabs";

export default {
   name: 'App',
   components: {
      // Tabs
   },

   data() {
      return {
         activeTab: true
      }
   }
}
</script>

<style lang="scss">
@import 'node_modules/bootstrap/scss/bootstrap.scss';
@import 'node_modules/bootstrap-vue/src/index.scss';
@import "./assets/fonts/Montserrat/stylesheet.css";
@import "./assets/fonts/SourceSansPro/stylesheet.css";


* {
   padding: 0;
   margin: 0;
   border: 0;
}


*,
*:before,
*:after {
   -webkit-box-sizing: border-box;
   -moz-box-sizing: border-box;
   box-sizing: border-box;
}


:focus,
:active {
   outline: none;
}

a:focus,
a:active {
   outline: none;
}


nav,
footer,
header,
aside {
   display: block;
}


html,
body {
   height: 100%;
   width: 100%;
   font-size: 100%;
   line-height: 1;
   font-size: 14px;
   -ms-text-size-adjust: 100%;
   -moz-text-size-adjust: 100%;
   -webkit-text-size-adjust: 100%;
}


input,
button,
textarea {
   font-family: inherit;
}


input::-ms-clear {
   display: none;
}

button {
   cursor: pointer;
}

button::-moz-focus-inner {
   padding: 0;
   border: 0;
}

a,
a:visited {
   text-decoration: none;
   color: #333333;
}

a:hover {
   text-decoration: none;
}

ul li {
   list-style: none;
}

img {
   vertical-align: top;
}

h1,
h2,
h3,
h4,
h5,
h6 {
   font-size: inherit;
   font-weight: 400;
   margin: 0;
}

// обнуление


body {
   font-family: 'Source Sans Pro', sans-serif;
   color: #333333;
   background-color: #EDEDED;

}

h1, h2, h3, h4, h5, h6 {
   font-family: Montserrat, sans-serif;
}

h6 {
   font-size: 19px;
}

.wrapper {
   max-width: 1070px;
   margin: 0 auto;
   //border: 1px solid red;
}

header {
   margin-bottom: 51px;
   background-color: #fff;

   .wrapper {
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: space-between;
   }

   .header__logo {
      max-height: 32px;
      max-width: 181px;
      width: 100%;
      height: 100%;
      background: url('./assets/svg/mf_logo_full.svg') center / contain no-repeat;
      fill: black;
   }
}

.big-title {
   text-align: center;
   padding: 0 30px;
   margin-bottom: 42px;

   h1 {
      font-size: 52px;
      line-height: 56px;
      font-weight: 900;
      color: #00B956;
   }
}

.tabs {
   font-size: 20px;
   display: flex;
   margin-bottom: 40px;

   div:first-child {
      border-right: 1px solid #D9D9D9;
   }

   div:last-child {
      border-left: 1px solid #D9D9D9;
   }

   .tabs__tab {
      width: 50%;
      background-color: #fff;
      height: 96px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-bottom: 4px solid transparent;
      transition: .3s;
      cursor: pointer;

      svg {
         fill: #333333;
         margin-right: 20px;
         transition: .3s;
      }
   }

   .tabs__tab.active {
      color: #00B956;
      border-bottom: 4px solid #00B956;

      svg {
         fill: #00B956;
      }
   }

}

.tab-content {
   padding: 30px 40px;
   background-color: #fff;

   &__questions {
      h3 {
         font-size: 24px;
         line-height: 56px;
         text-align: center;
         border-bottom: 1px solid #D9D9D9;
         margin-bottom: 27px;

         span {
            background: #fff url() 0 0 no-repeat;
         }
      }

      p {
         font-size: 19px;
         margin-bottom: 28px;
      }

      .tab-content__collapse {
         .card {
            background-color: #F9F9F9;
            padding: 15px 16px;
            border: 0;
            border-radius: 0;
         }

         &_qustion {
            color: #34AAF2;
            line-height: 36px;
         }

         &_answer {
            line-height: 20px;
         }
      }
   }
}


</style>
