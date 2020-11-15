<template>
   <div id="app">

      <header>
         <div class="wrapper">
            <a href="#" class="header__logo"></a>
            <h6 class="header__phone">
               <a href="tel:8 800 55-00-001">8 800 55-00-001</a>
            </h6>
            <a class="header__phone-mobile" href="tel:8 800 55-00-001">
               <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32">
                  <defs></defs>
                  <g transform="translate(-4 -4)">
                     <path class="a" d="M17,6V4A19,19,0,0,1,36,23H34A17,17,0,0,0,17,6Z"/>
                     <path class="a" d="M17,18V16a7,7,0,0,1,7,7H22A5,5,0,0,0,17,18Z"/>
                     <path class="a" d="M17,12V10A13,13,0,0,1,30,23H28A11,11,0,0,0,17,12Z"/>
                     <path class="a"
                           d="M21.48,36h1L26,32.44l-6.83-6.83-2.78,2.78a12.52,12.52,0,0,1-4.94-4.78l2.78-2.78L7.56,14,4,17.56v1A17.71,17.71,0,0,0,21.48,36ZM6,18.38l1.56-1.56,3.85,4L9,23.23l.33.65a14.79,14.79,0,0,0,6.79,6.63l.65.33,2.4-2.4,4,4L21.62,34h-.14A15.6,15.6,0,0,1,6,18.52Z"/>
                  </g>
               </svg>
            </a>
         </div>
      </header>

      <div class="wrapper">
         <div class="big-title">
            <h1>Помощь и обслуживание клиентов</h1>
         </div>
         <Tabs
            @clickQuestion="activeTab = true"
            @clickInstruction="activeTab = false"
         />
         <MySelect @checkOptions="checkOptions"/>

         <div v-if="activeTab" class="tab-content">
            <div class="tab-content__questions">
               <h3>Вопросы по темам <span></span></h3>
               <div v-for="(question, index) in questions" :key="index" class="tab-content__collapse">
                  <p v-b-toggle="'collapse' + index">
                     {{ question.title }}
                     <span class="toggle"></span>
                  </p>
                  <b-collapse :id="'collapse' + index">
                     <div v-for="(question, index) in question.question"
                          :key="index"
                          class="tab-content__collapse_qustion">
                        <div>
                           <span v-b-toggle="'collapse-2-' + question.id">
                              {{ question.question }}
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
import Tabs from "@/components/Tabs";
import MySelect from "@/components/MySelect";

export default {
   name: 'App',
   components: {
      Tabs,
      MySelect
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
   },
   methods: {
      checkOptions(option) {
         option ? this.activeTab = false : this.activeTab = true
      }
   }
}
</script>

<style lang="scss">
@import 'node_modules/bootstrap/scss/bootstrap.scss';
// bootstrap
@import 'node_modules/bootstrap-vue/src/index.scss';
// bootstrap
@import "./assets/fonts/Montserrat/stylesheet.css";
// шрифт
@import "./assets/fonts/SourceSansPro/stylesheet.css";
// шрифт
@import "./assets/scss/null.scss"; // обнуление

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
   max-width: 1100px;
   margin: 0 auto;
   padding: 0 15px;
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

   .header__phone a:hover {
      color: inherit;
   }

   a.header__phone-mobile {
      display: none;
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
         margin-bottom: 5px;
      }

      p {
         font-size: 19px;
         padding: 28px 16px 28px 0;
         margin: 0;
         display: flex;
         align-items: center;
         height: 79px;
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
         position: relative;
         z-index: 0;

         > div {
            padding: 15px 16px;

            > span {
               cursor: pointer;
               color: #34AAF2;
            }
         }
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
               height: calc(100% - 15px);
               top: 0;
               left: 0;
               z-index: -1;
               background-color: #F9F9F9;
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
         text-align: center;
         margin-right: 30px;

         img {
            max-width: 62px;
            max-height: 45px;
         }
      }

      .tab-content__collapse_qustion {
         padding: 15px 16px;

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


@media (max-width: 767px) {
   header {
      margin-bottom: 21px;

      .wrapper {
         height: 64px;
      }

      .header__logo {
         max-height: 24px;
         max-width: 135px;
      }

      h6 {
         display: none;
      }

      a.header__phone-mobile {
         display: block;
         width: 32px;
         height: 32px;
         margin-right: 18px;

         svg {
            display: block;
         }
      }

   }

   .big-title {
      padding: 0;
      margin-bottom: 22px;

      h1 {
         font-size: 30px;
         line-height: 36px;
         font-weight: 900;
         color: #00B956;
      }
   }

   .tab-content {
      background-color: transparent;
      padding: 0;

      &__questions {

         h3 {
            font-size: 19px;
            line-height: 23px;
            border-bottom: 0;
            margin-bottom: 13px;
         }

         .tab-content__collapse {
            background-color: #fff;
            padding: 0;

            &:last-child {
               border-bottom: 1px solid transparent;
            }

            > .collapse {
               padding: 0 8px;

               .collapse {
                  margin-bottom: 0 !important;
               }
            }
         }

         p {
            font-size: 16px;
            padding: 0 20px 0 15px;
            margin: 0;
            height: 61px;
         }

         .tab-content__collapse_answer {
            padding: 0 11px;
         }

         .tab-content__collapse_asset {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            padding-bottom: 15px;

            span {
               line-height: 18px;
               margin-bottom: 7px;
            }

            span:nth-child(1) {
               width: 100%;
               text-align: center;
               margin-right: 0 !important;
            }

            span:nth-child(2) {
               margin-right: 56px !important;
            }

         }

         .tab-content__collapse_qustion > span {
            line-height: 18px;
            padding-right: 20px;
            display: inline-block;
         }
      }

      &__directions {
         border: 0;

         .collapse__img {
            width: 36px;
            margin-right: 13px;

            img {
               max-width: 36px;
               max-height: 30px;
            }
         }
      }
   }

   .copyright {
      margin-bottom: 35px;
   }
}


</style>
