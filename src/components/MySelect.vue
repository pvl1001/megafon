<template>
   <div class="select">
      <div class="select__arrow" :class="{open: openSelect}"></div>
      <div v-if="selected"
           @click="showOptions"
           class="select__option">
         <svg xmlns="http://www.w3.org/2000/svg" width="29" viewBox="0 0 29 24.379">
            <defs></defs>
            <g transform="translate(-1 -3.596)">
               <path class="a" d="M19.9,20.56,18.43,19,17,20.38,19.45,23h.89l4.44-4.68-1.46-1.38Z"/>
               <path class="a"
                     d="M28.43,22.61A8.291,8.291,0,0,0,18.7,11.58,8.358,8.358,0,1,0,2,12.33a8.25,8.25,0,0,0,.54,2.94L1,18l2,2.71,3.58-1a8.2,8.2,0,0,0,5.77.68,8.32,8.32,0,0,0,12.1,6.66l3.32.92L30,25.5ZM7.19,17.81l-.29-.17-3.09.78-.49-.65L4.76,15.3l-.18-.41A6.36,6.36,0,1,1,7.2,17.81ZM27,25.7l-2.84-.77-.36.21a6.32,6.32,0,0,1-9.51-5.46,8.35,8.35,0,0,0,4.28-6,6.33,6.33,0,0,1,7.84,8.55l-.18.41,1.17,2.55Z"/>
               <circle class="a" cx="1.1" cy="1.1" r="1.1" transform="translate(9.27 14.9)"/>
               <path class="a" d="M10.37,14H9.49V12h.87a1,1,0,1,0-1-1h-2a3,3,0,1,1,3,3Z"/>
            </g>
         </svg>
         Часто задаваемые вопрососы
      </div>
      <div v-else
           @click="showOptions"
           class="select__option">
         <svg xmlns="http://www.w3.org/2000/svg" width="17" viewBox="0 0 17 24">
            <defs></defs>
            <rect class="a" width="7" height="2" transform="translate(4 5)"/>
            <rect class="a" width="8" height="2" transform="translate(4 9)"/>
            <rect class="a" width="4" height="2" transform="translate(4 13)"/>
            <path class="a" d="M17,13V0H0V24H17Zm-2,9H2V2H15V22Zm1.5,0h0"/>
         </svg>
         Инструкции
      </div>

      <input name="test" type="radio" id="question" :value="true" v-model="selected">
      <label :class="{open: !selected && openSelect}" for="question">
         <div
            @click="checkOptions"
            class="select__option">
            <svg xmlns="http://www.w3.org/2000/svg" width="29" viewBox="0 0 29 24.379">
               <defs></defs>
               <g transform="translate(-1 -3.596)">
                  <path class="a" d="M19.9,20.56,18.43,19,17,20.38,19.45,23h.89l4.44-4.68-1.46-1.38Z"/>
                  <path class="a"
                        d="M28.43,22.61A8.291,8.291,0,0,0,18.7,11.58,8.358,8.358,0,1,0,2,12.33a8.25,8.25,0,0,0,.54,2.94L1,18l2,2.71,3.58-1a8.2,8.2,0,0,0,5.77.68,8.32,8.32,0,0,0,12.1,6.66l3.32.92L30,25.5ZM7.19,17.81l-.29-.17-3.09.78-.49-.65L4.76,15.3l-.18-.41A6.36,6.36,0,1,1,7.2,17.81ZM27,25.7l-2.84-.77-.36.21a6.32,6.32,0,0,1-9.51-5.46,8.35,8.35,0,0,0,4.28-6,6.33,6.33,0,0,1,7.84,8.55l-.18.41,1.17,2.55Z"/>
                  <circle class="a" cx="1.1" cy="1.1" r="1.1" transform="translate(9.27 14.9)"/>
                  <path class="a" d="M10.37,14H9.49V12h.87a1,1,0,1,0-1-1h-2a3,3,0,1,1,3,3Z"/>
               </g>
            </svg>
            Часто задаваемые вопрососы
         </div>
      </label>

      <input name="test" type="radio" id="instructions" :value="false" v-model="selected">
      <label :class="{open: selected && openSelect}" for="instructions">
         <div
            @click="checkOptions"
            class="select__option">
            <svg xmlns="http://www.w3.org/2000/svg" width="17" viewBox="0 0 17 24">
               <defs></defs>
               <rect class="a" width="7" height="2" transform="translate(4 5)"/>
               <rect class="a" width="8" height="2" transform="translate(4 9)"/>
               <rect class="a" width="4" height="2" transform="translate(4 13)"/>
               <path class="a" d="M17,13V0H0V24H17Zm-2,9H2V2H15V22Zm1.5,0h0"/>
            </svg>
            Инструкции
         </div>
      </label>

   </div>
</template>

<script>
export default {
   name: "MySelect",
   data() {
      return {
         selected: true,
         openSelect: false
      }
   },
   methods: {
      showOptions() {
         this.openSelect = !this.openSelect
      },
      checkOptions() {
         this.showOptions()
         this.$emit('checkOptions', this.selected)
      }
   }
}
</script>

<style scoped lang="scss">

.select {
   display: none;
}

@media (max-width: 767px) {

   .select {
      display: block;
      width: 100%;
      margin-bottom: 43px;
      position: relative;

      > div.select__option {
         color: #00B956;

         svg {
            fill: #00B956;
         }
      }

      &__arrow {
         position: absolute;
         right: 28px;
         top: 27px;
         width: 9px;
         height: 9px;
         background: url('../assets/svg/select-arrow.svg') center / contain no-repeat;
         transition: .3s;
      }

      &__arrow.open {
         transform: rotateX(180deg);
      }

      input {
         display: none;
      }

      label {
         display: block;
         visibility: hidden;
         overflow: hidden;
         height: 0;
         transition: .3s;
         margin-bottom: 0;
      }

      label.open {
         visibility: visible;
         height: 58px;
      }

      &__option {
         width: 100%;
         height: 58px;
         background-color: #fff;
         padding: 0 40px 0 24px;
         font-size: 15px;
         font-weight: 600;
         line-height: 19px;
         display: flex;
         align-items: center;
         border: 1px solid #D8D8D8;

         svg {
            margin-right: 10px;
            fill: #333;
         }
      }
   }
}


</style>