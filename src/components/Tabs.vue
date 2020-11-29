<template>
   <div class="tabs">
      <div @click="clickQuestion" class="tabs__tab" :class="{active: activeTab}">
<!--         <svg xmlns="http://www.w3.org/2000/svg" width="37" height="31" viewBox="0 0 29 24.379">-->
<!--            <defs></defs>-->
<!--            <g transform="translate(-1 -3.596)">-->
<!--               <path class="a" d="M19.9,20.56,18.43,19,17,20.38,19.45,23h.89l4.44-4.68-1.46-1.38Z"/>-->
<!--               <path class="a"-->
<!--                     d="M28.43,22.61A8.291,8.291,0,0,0,18.7,11.58,8.358,8.358,0,1,0,2,12.33a8.25,8.25,0,0,0,.54,2.94L1,18l2,2.71,3.58-1a8.2,8.2,0,0,0,5.77.68,8.32,8.32,0,0,0,12.1,6.66l3.32.92L30,25.5ZM7.19,17.81l-.29-.17-3.09.78-.49-.65L4.76,15.3l-.18-.41A6.36,6.36,0,1,1,7.2,17.81ZM27,25.7l-2.84-.77-.36.21a6.32,6.32,0,0,1-9.51-5.46,8.35,8.35,0,0,0,4.28-6,6.33,6.33,0,0,1,7.84,8.55l-.18.41,1.17,2.55Z"/>-->
<!--               <circle class="a" cx="1.1" cy="1.1" r="1.1" transform="translate(9.27 14.9)"/>-->
<!--               <path class="a" d="M10.37,14H9.49V12h.87a1,1,0,1,0-1-1h-2a3,3,0,1,1,3,3Z"/>-->
<!--            </g>-->
<!--         </svg>-->
         Часто задаваемые вопросы
      </div>
      <div @click="clickInstruction" class="tabs__tab" :class="{active: !activeTab}">
<!--         <svg xmlns="http://www.w3.org/2000/svg" width="22" height="31" viewBox="0 0 17 24">-->
<!--            <defs></defs>-->
<!--            <rect class="a" width="7" height="2" transform="translate(4 5)"/>-->
<!--            <rect class="a" width="8" height="2" transform="translate(4 9)"/>-->
<!--            <rect class="a" width="4" height="2" transform="translate(4 13)"/>-->
<!--            <path class="a" d="M17,13V0H0V24H17Zm-2,9H2V2H15V22Zm1.5,0h0"/>-->
<!--         </svg>-->
         Инструкции
      </div>
   </div>
</template>

<script>
export default {
   name: "Tabs",
   data() {
      return {
         activeTab: true,
      }
   },
   methods: {
      clickQuestion() {
         this.activeTab = true
         this.$emit('clickQuestion')
      },
      clickInstruction() {
         this.activeTab = false
         this.$emit('clickInstruction')
      }
   }
}
</script>

<style lang="scss">

.tabs {
   font-size: 15px;
   display: flex;
   align-items: center;

   .tabs__tab {
      background-color: #fff;
      color: #ADADAD;
      display: flex;
      align-items: center;
      justify-content: center;
      border-bottom: 2px solid transparent;
      transition: .3s;
      cursor: pointer;
      height: 35px;
      margin-right: 35px;
      letter-spacing: 0.2px;
      font-weight: 600;

      &:last-child {
         margin-right: 0;
      }

      svg {
         fill: #333333;
         margin-right: 20px;
         transition: .3s;
      }
   }

   .tabs__tab.active {
      color: #333;
      border-bottom: 2px solid #00B956;

      svg {
         fill: #00B956;
      }
   }

}

</style>