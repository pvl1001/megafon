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

      <section class="section-1">
         <div class="big-title">
            <div class="wrapper">
               <h1>Помощь и обслуживание клиентов</h1>
               <Tabs
                  @clickQuestion="activeTab = true"
                  @clickInstruction="activeTab = false"
               />
            </div>
         </div>
         <div class="wrapper">
            <div v-if="activeTab" class="FAQ">
               <h2>Вопросы по темам</h2>
               <div class="tab-content">
                  <div class="tab-content__questions">
                     <div v-for="(question, index) in questions" :key="index" class="tab-content__collapse">
                        <p v-b-toggle="'collapseFAQ' + index">
                           {{ question.title }}
                           <span class="toggle"></span>
                        </p>
                        <b-collapse :id="'collapseFAQ' + index">
                           <div v-for="(question, index) in question.question"
                                :key="index"
                                class="tab-content__collapse_question">
                              <div>
                                 <span v-b-toggle="'collapseFAQ-2-' + question.id">
                                 {{ question.question }}
                              </span>
                                 <div class="btns-question">
                                    <div class="btns-question__share">
                                       <div @click="clickCopy(question.id)"
                                            class="btns-question__share_copy">
                                          Копировать ссылку
                                       </div>
                                    </div>
                                    <div v-b-toggle="'collapseFAQ-2-' + question.id" class="btns-question__close"></div>
                                 </div>
                                 <b-collapse :id="'collapseFAQ-2-' +  question.id" class="tab-content__collapse_answer">
                                    <span v-html="question.answer"></span>
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
               <div :class="{ show: showMessCopy }" class="copyMessage">Ссылка скопирована в буфер обмена</div>
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
                           <div class="tab-content__collapse_question">
                              <a href="#">– Открыть инструкцию</a>
                           </div>
                           <div class="tab-content__collapse_question">
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

            <div class="supports">
               <h2>Не нашли что искали?</h2>
               <div class="supports__block">
                  <a href="#">Онлайн-чат с поддержкой</a>
               </div>
            </div>

            <div class="copyright">
               6+© 2020 ПАО «МегаФон»<br>
               Продолжая использовать наш сайт, вы даете согласие на обработку файлов Cookies и
               других пользовательских данных, в соответствии с <a href="#">Политикой конфиденциальности.</a>
            </div>
         </div>
      </section>

   </div>
</template>

<script>
import Tabs from "@/components/Tabs";

export default {
   name: 'App',
   components: {
      Tabs,
   },

   data() {
      return {
         closePlaceCopy: [],
         showMessCopy: false,
         activeTab: true,
         reviewSent: false,
         questions: [
            {
               title: 'Оплата, баланс, счет',
               question: [
                  {
                     id: 1,
                     question: 'Как узнать свой лицевой счет?',
                     answer: 'Номер телефона — это ваш лицевой счёт. С его помощью можно оплатить услуги, войти в личный кабинет и в МегаФон ТВ. ',
                     reviewSent: null
                  },
                  {
                     id: 2,
                     question: 'Как проверить баланс?',
                     answer: 'Проверить баланс можно в голосовом меню с помощью USSD команды *100# или в личном кабинете. ',
                     reviewSent: null
                  },
                  {
                     id: 3,
                     question: 'Как пополнить баланс?',
                     answer: 'Пополнить баланс можно несколькими способами: <br>1. В Личном кабинете: банковской картой, электронным кошельком, по номер у телефона.<br>' +
                        '2. В приложении Сбербанк-онлайн, раздел «Платеж или перевод». Найдите в списке платежей «Интернет и ТВ», укажите поставщика услуг МегаФон, введите номер лицевого счёта и сумму оплаты.<br>' +
                        '3. Наличными через терминалы оплаты: Qiwi, CyberPlat или Элексент, банкоматы Сбербанка России и Московского кредитного банка или пункты приема платежей: Мегафон Ритейл, Связной',
                     reviewSent: null
                  },
                  {
                     id: 4,
                     question: 'Что такое автоплатеж и как его подключить?',
                     answer: 'Автоплатеж - это сервис, позволяющий настроить автоматическое пополнение счета с вашей банковской карты. Его можно подключить в личном кабинете. \n' +
                        'Данные карты защищены, а переводы зашифрованы, поэтому это совершенно безопасно. Вы сами выбираете, когда и на какую сумму пополнять счёт, и в любой момент можете изменить настройки.\n' +
                        'Дата списания абонентской платы соответствует дате подключения тарифа.',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Мегафон ТВ',
               question: [
                  {
                     id: 5,
                     question: '– Что такое Мегафон ТВ?',
                     answer: 'Мегафон ТВ - это онлайн-кинотеатр, который уже доступен в вашем тарифе (кроме тарифов #ДляДомаИнтернет, и Объединяй!Два Интернета).',
                     reviewSent: null
                  },
                  {
                     id: 6,
                     question: '- Как зарегистрироваться?',
                     answer: 'Введите номер телефона в сервисе Мегафон ТВ, задайте числовой пароль и введите код подтверждения, полученный в SMS. Логин – ваш номер телефона',
                     reviewSent: null
                  },
                  {
                     id: 7,
                     question: '- Где смотреть?',
                     answer: 'Сервисом Мегафон ТВ можно воспользоваться на ТВ-приставке, Smart TV, Android TV, в смартфоне, планшете и браузере, для этого нужно скачать приложение в официальных магазинах ваших устройств. Если телевизор не поддерживает функцию Smart TV или поддерживает, но вы захотите подключить ещё один, понадобится дополнительная приставка. Чтобы её заказать, звоните нам: 8 800 550-00-01',
                     reviewSent: null
                  }
               ]
            },
            {
               title: 'Добровольная блокировка',
               question: [
                  {
                     id: 8,
                     question: '- Что такое добровольная блокировка и как ее подключить?',
                     answer: '',
                     reviewSent: null
                  }
               ]
            },
            {
               title: 'Вопросы по работе интернета',
               question: [
                  {
                     id: 9,
                     question: '- Что делать, если не работает интернет?',
                     answer: 'Перед обращением в техническую поддержку, пожалуйста, проделайте следующие действия:<br>' +
                        '1) перезагрузите оборудование<br>' +
                        '2) проверьте баланс (ссылка на вход в веб лк)<br>' +
                        '3) проверьте целостность кабеля, коннектора<br>' +
                        '4) убедитесь, что интернет-кабель подключен к роутеру',
                     reviewSent: null
                  },
                  {
                     id: 10,
                     question: '- Правда, что для роутера нужно правильно выбрать место?',
                     answer: 'Стены дома или квартиры существенно ухудшают Wi-Fi сигнал, поэтому чем ближе роутер к устройству, тем лучше качество соединения. Советуем установить устройство в центре квартиры, это увеличит площадь покрытия Wi-Fi.',
                     reviewSent: null
                  },
                  {
                     id: 11,
                     question: '- Что делать при низкой скорости или помехах?',
                     answer: 'Скорость может снизиться по одной из следующих причин:<br>' +
                        '- устаревшее/неподходящее оборудование <br>' +
                        '- неправильное расположение роутера <br>' +
                        '- работа другой программы, загружающей интернет-канал (например, Торрент)<br>' +
                        '- наличие вредоносного ПО на компьютере<br>' +
                        '- работа программ защиты<br>' +
                        '- ограничения по скорости на сервере или перегруженность сервера<br>' +
                        '<br>' +
                        'Что может помочь:<br>' +
                        '- убедитесь, что пропускная способность роутера подходит для вашего тарифа<br>' +
                        '- расположите роутер ближе, устраните преграды<br>' +
                        '- перезагрузите роутер или подключитесь напрямую<br>' +
                        '- если доступно 2 подключения, переключитесь с 2.4 ГГц на частоту 5 ГГц<br>' +
                        '- выключите другие программы, использующие интернет-канал, и <a href="#">проверьте скорость</a> заново<br>' +
                        '- проверьте наличие вредоносного ПО с помощью антивируса<br>' +
                        '- временно отключите программу защиты (firewall, антивирусы и т.п.) и <a href="#">проверьте скорость</a>',
                     reviewSent: null
                  },
                  {
                     id: 12,
                     question: '- Что необходимо при обращении в ТП?',
                     answer: '1) Находиться возле оборудования<br> ' +
                        '2) Назвать адрес подключения/номер договора<br> ' +
                        '3) Назвать код ошибки или надпись на экране или прислать скриншот<br> ' +
                        '4) Сообщить, если у вас уже есть зафиксированное обращение по данному вопросу<br> ' +
                        '5) Описать действия, которые вы уже предприняли и их результат',
                     reviewSent: null
                  },
                  {
                     id: 13,
                     question: '- Как настроить интернет-соединение?',
                     answer: 'Для подключения интернет-соединения напрямую воспользуйтесь нашими инструкциями (ссылка на раздел с инструкцией по подключению напрямую)',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Перезд вместе с нами',
               question: [
                  {
                     id: 14,
                     question: '- Как переехать без потери интернета?',
                     answer: '',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Статический IP адрес',
               question: [
                  {
                     id: 15,
                     question: '- Что такое статический IP адрес?',
                     answer: 'Это постоянный IP-адрес, закрепленный на время пользования услуги.  С ним у вас будет удаленный доступ к закрытым ресурсам сети, вы сможете организовывать собственные игровые и web серверы и играть в многопользовательские игры. Услуга включена в стоимость тарифа.',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Обрудование',
               question: [
                  {
                     id: 16,
                     question: '- Как выбрать оборудование?',
                     answer: 'Важно помнить, что скорость домашнего интернета зависит от пропускной способности роутера.<br>' +
                        'Например, для тарифов со скоростью 100 Мбит/с не подойдет роутер с пропускной способностью до 100 Мбит/с. Также не рекомендуем пользоваться устаревшими моделями.<br>' +
                        '<br>' +
                        'Для домашнего интернета вы можете использовать свой роутер, но для стабильности сигнала мы рекомендуем пользоваться роутером, который предлагается в выбранном тарифе',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Увеличение скорости интернета',
               question: [
                  {
                     id: 16,
                     question: '- Как увеличить скорость интернета?',
                     answer: '',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Антивирус',
               question: [
                  {
                     id: 17,
                     question: '- Как подключить антивирус?',
                     answer: 'Антивирус уже входит в ваш тариф, вы можете подключить от одного до трёх устройств.',
                     reviewSent: null
                  },
               ]
            },
            {
               title: 'Скидки близким',
               question: [
                  {
                     id: 18,
                     question: '- Как подключить всю семью к Мегафону со скидкой 40%?',
                     answer: 'Абоненты тарифов «Объединяй» могут подключить своих близких к тарифу «Без переплат.Всё» со скидкой 40% навсегда. Оплата каждой дополнительной sim  карты производится отдельно.  Для получения дополнительной информации и подключения: <br>' +
                        '1. Позвоните по номеру 8 800 550-00-01.<br>' +
                        '2. Закажите SIM-карту (максимум — 10 штук) с тарифом «Без переплат. Всё».<br>' +
                        '3. Дождитесь сотрудника с SIM-картой и заявлением о переносе номера, если необходимо его сохранить.',
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
      clickCopy() { // копировать ссылку
         this.showMessCopy = true
         setTimeout(() => {
            this.showMessCopy = false
         }, 2500)
      }
   },
   mounted() {
      let arr = document.querySelectorAll('.btns-question__share')
      window.addEventListener('click', function (e) {
         arr.forEach(el => { // показать кнопку копировать
            if (e.target !== el) {
               el.childNodes[0].classList.remove('show')
            } else el.childNodes[0].classList.add('show')
         })
      })
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
   background-color: #fff;
   position: relative;
   box-shadow: 0 0 15px #00000026;

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

   .header__phone a {
      font-weight: 500;
   }

   .header__phone a:hover {
      color: inherit;
   }

   a.header__phone-mobile {
      display: none;
   }

}

.section-1 {
   padding-bottom: 31px;
}

.big-title {
   margin-bottom: 28px;
   background-color: #fff;

   h1 {
      font-size: 52px;
      line-height: 56px;
      font-weight: 900;
      max-width: 760px;
      padding: 42px 0 25px;
   }
}

.FAQ h2 {
   font-size: 24px;
   margin-bottom: 16px;
}

.tab-content {
   padding: 30px 40px;
   background-color: #fff;
   margin-bottom: 23px;

   &__questions {
      border-top: 1px solid #D9D9D9;

      h3 {
         font-size: 24px;
         line-height: 69px;
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
         min-height: 79px;
      }

      .toggle {
         display: block;
         width: 20px;
         height: 20px;
         background: url('./assets/svg/downarrow_121316.svg') center / 13px no-repeat;
         opacity: .7;
         transform: rotateX(20deg);
         margin-left: auto;
         flex-shrink: 0;
      }

      p.not-collapsed .toggle {
         transform: rotateX(160deg);
      }

      .tab-content__collapse_question {
         position: relative;
         z-index: 0;

         > div {
            padding: 15px 16px;

            > span {
               display: inline-block;
               cursor: pointer;
               color: #34AAF2;
               line-height: 18px;
               padding-right: 20px;
            }
         }
      }

      .tab-content__collapse {
         border-bottom: 1px solid #D9D9D9;
         padding: 0 15px;

         .collapse.show {

            .btns-question {
               position: absolute;
               top: 15px;
               right: 17px;
               transition: .1s;
               opacity: 0;
               visibility: hidden;
               display: flex;
               cursor: auto;

               &__share {
                  width: 17px;
                  height: 17px;
                  background: url('./assets/svg/share.svg') center / 12px no-repeat;
                  margin-right: 33px;
                  cursor: pointer;
                  position: relative;

                  &_copy {
                     height: 53px;
                     width: 198px;
                     border-radius: 9px;
                     padding-left: 42px;
                     position: absolute;
                     display: flex;
                     align-items: center;
                     z-index: 1;
                     right: 0;
                     top: -20px;
                     box-shadow: 0 0 15px #00000026;
                     background: #fff url('./assets/svg/copy.svg') 15px center / 18.4px no-repeat;
                     opacity: 0;
                     visibility: hidden;
                  }

                  &_copy.show {
                     opacity: 1;
                     visibility: visible;
                  }
               }

               &__close {
                  width: 17px;
                  height: 17px;
                  background: url('./assets/svg/cross.svg') center / cover no-repeat;
                  cursor: pointer;
                  opacity: .5;
               }
            }

            &:last-child {
               margin-bottom: 15px;
            }

            span.not-collapsed {
               padding-right: 70px;
            }

            span.not-collapsed + .btns-question {
               opacity: 1;
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

               a {
                  color: #34AAF2;
               }
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

      p {
         padding: 25px 17px 28px 5px;
      }

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

      .tab-content__collapse_question {
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

.copyMessage {
   width: 343px;
   line-height: 90px;
   text-align: center;
   border-radius: 9px;
   background-color: #00B956;
   color: #fff;
   position: fixed;
   left: calc(50% - 171px);
   transition: .3s;
   bottom: -90px;
   opacity: 0;

   &.show {
      bottom: 50px;
      opacity: 1;
   }
}

.supports {
   margin-bottom: 40px;

   h2 {
      font-size: 24px;
      margin-bottom: 16px;
   }

   &__block {
      background-color: #fff;
      padding: 19px 41px;

      a {
         display: inline-block;
         height: 24px;
         line-height: 24px;
         padding-left: 50px;
         color: #34AAF2;
         font-size: 16px;
         background: #fff url('./assets/svg/Support-avatar_24.svg') 0 50% / contain no-repeat;
      }
   }
}

.copyright {
   font-size: 12px;
   line-height: 16px;
   max-width: 548px;

   a {
      color: #34AAF2;
   }
}


@media (max-width: 767px) {
   header {

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
      margin-bottom: 35px;

      h1 {
         padding: 30px 0 25px;
         font-size: 30px;
         line-height: 36px;
      }
   }

   h2 {
      font-size: 19px !important;
   }

   .tab-content {
      background-color: transparent;
      padding: 0;
      margin-bottom: 43px;


      &__questions {
         border-top: 0;

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
            padding: 10px 20px 10px 15px;
            margin: 0;
            min-height: 61px;
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

         .tab-content__collapse_question > span {
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

   .copyMessage {
      width: calc(100% - 30px);
      left: 15px;

      &.show {
         bottom: 30px;
      }
   }

   .supports__block {
      padding: 19px 17px;

      a {
         padding-left: 44px;
      }
   }

   .copyright {
      margin-bottom: 35px;
   }
}


</style>
