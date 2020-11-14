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
            <div  class="tab-content__questions">
               <h3>Вопросы по темам <span></span></h3>
               <div v-for="(question, index) in questions" :key="index" class="tab-content__collapse">
                  <p v-b-toggle="'collapse' + index">
                     {{ question.title }}
                     <span class="toggle"></span>
                  </p>
                  <b-collapse :id="'collapse' + index">
                     <div  v-for="(question, index) in question.question"
                           :key="index"
                           class="tab-content__collapse_qustion">
                        <span v-b-toggle="'collapse-2-' + question.id">
                           {{question.question}}
                        </span>
                        <div v-b-toggle="'collapse-2-' +  question.id" class="close-question"></div>
                        <b-collapse :id="'collapse-2-' +  question.id" class="tab-content__collapse_answer">
                           <span>
                              {{ question.answer }}
                           </span>
                           <div v-if="!question.reviewSent" class="tab-content__collapse_asset">
                              <span>Информация была полезной?</span>
                              <span @click="question.reviewSent = !question.reviewSent">Да</span>
                              <span @click="question.reviewSent = !question.reviewSent">Нет</span>
                           </div>
                           <div v-if="question.reviewSent" class="tab-content__collapse_asset">
                              <span>Отзыв отправлен. Спасибо!</span>
                           </div>
                        </b-collapse>
                     </div>
                  </b-collapse>

               </div>
            </div>
         </div>
         <div v-if="!activeTab" class="tab-content">
            <div class="tab-content__directions">
               <div class="tab-content__questions">
                  <div v-for="(instructions, index) in instructions"
                       :key="index" class="tab-content__collapse">
                     <p v-b-toggle="'collapse' + index">
                         <span class="collapse__img">
                           <img :src="require('./assets/img/' + instructions.img)" alt="img">
                        </span>
                        {{ instructions.title }}
                        <span class="toggle"></span>
                     </p>
                     <b-collapse :id="'collapse' + index">
                        <div class="tab-content__collapse_qustion">
                           <a href="#">– Открыть инструкцию</a>
                        </div>
                        <div class="tab-content__collapse_qustion">
                           <span>
                              <a href="#">– Скачать</a>
                              <span>(PDF, 0.4 MB)</span>
                           </span>
                        </div>
                     </b-collapse>
                  </div>
               </div>
            </div>
         </div>

         <div class="copyright">
            6+© 2020 ПАО «МегаФон»<br>
            Продолжая использовать наш сайт, вы даете согласие на обработку файлов Cookies и
            других пользовательских данных, в соответствии с <a href="#">Политикой конфиденциальности.</a>
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
         activeTab: true,
         reviewSent: false,
         questions: [
            {
               title: 'МегаФон ТВ',
               question: [
                  {
                     id: 1,
                     question: '– Что такое МегаФон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 2,
                     question: '– Как зарегистрироваться в Мегафон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 3,
                     question: '– Где скачать приложение Мегафон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 4,
                     question: '– Как проверить баланс?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Домашний интернет',
               question: [
                  {
                     id: 5,
                     question: '– Что такое МегаФон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 6,
                     question: '– Как зарегистрироваться в Мегафон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 7,
                     question: '– Где скачать приложение Мегафон ТВ?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
                  {
                     id: 8,
                     question: '– Как проверить баланс?',
                     answer: 'МегаФон ТВ — это пакеты с новинками кино и сериалов, детскими, познавательными программами, новостями и спортом. Оформите подписку в приложении МегаФон ТВ и смотрите на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере',
                     reviewSent: null
                  },
               ]
            }
         ],
         instructions: [
            {
               img: 'img1.png',
               title: 'Q5 MegaFon ТВ-приставка',
            },
            {
               img: 'img2.png',
               title: 'Роутер FR100-1',
            },
            {
               img: 'img3.png',
               title: 'Роутер FR1000-1',
            },
         ]
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
   margin-bottom: 52px;

   &__questions {
      h3 {
         font-size: 24px;
         line-height: 56px;
         text-align: center;
         border-bottom: 1px solid #D9D9D9;
      }

      p {
         font-size: 19px;
         padding: 28px 16px 28px 0;
         margin: 0;
         display: flex;
         align-items: center;
      }

      .toggle {
         display: block;
         width: 20px;
         height: 20px;
         background: url('./assets/svg/downarrow_121316.svg') center / 13px no-repeat;
         transition: .5s;
         opacity: .7;
         transform: rotateX(20deg);
         margin-left: auto;
      }

      p.not-collapsed .toggle {
         transform: rotateX(160deg);
      }

      .tab-content__collapse_qustion {
         padding: 15px 16px;
         position: relative;
         z-index: 0;
      }

      .tab-content__collapse {
         border-bottom: 1px solid #D9D9D9;
         padding: 0 15px;


         .collapse.show {

            .close-question {
               width: 17px;
               height: 17px;
               background: url('./assets/svg/cross.svg') center / cover no-repeat;
               position: absolute;
               top: 15px;
               right: 17px;
               transition: .1s;
               opacity: 0;
               visibility: hidden;
            }

            &:last-child {
               margin-bottom: 15px;
            }


            span.not-collapsed + .close-question {
               opacity: .5;
               visibility: visible;
            }


            span.not-collapsed:before {
               content: '';
               position: absolute;
               width: 100%;
               height: 100%;
               top: 0;
               left: 0;
               z-index: -1;
               background-color: #F9F9F9;
            }
         }

         &_qustion {
            > span {
               cursor: pointer;
               color: #34AAF2;
            }
         }

         &_answer {
            line-height: 20px;
            padding: 0 14px;

            > span {
               display: inline-block;
               margin: 15px 0 40px;

            }

            .tab-content__collapse_asset {
               span {
                  color: #34AAF2;
                  cursor: pointer;

                  &:nth-child(1) {
                     color: #999999;
                     margin-right: 24px;
                     cursor: initial;
                  }

                  &:nth-child(2) {
                     margin-right: 11px;
                  }
               }
            }
         }
      }
   }

   &__directions {
      border-top: 1px solid #D9D9D9;

      .collapse__img {
         display: block;
         width: 62px;
         margin-right: 30px;

         img {
            max-width: 100%;
            max-height: 100%;
         }
      }

      .tab-content__collapse_qustion {
         a {
            color: #34AAF2;
            margin-right: 5px;
         }

         a + span {
            color: #333333;
            cursor: auto;
         }
      }
   }
}

.copyright {
   font-size: 12px;
   line-height: 16px;
   max-width: 548px;
   margin-bottom: 25px;

   a {
      color: #34AAF2;
   }
}


</style>
