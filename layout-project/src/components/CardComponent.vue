<template>
  <div class="container p-0">
    <div class="row">
      <div class="mt-4 ms-2 text-center status-block" v-if="cardInformation.status">
        <h3 class="mt-1">{{cardInformation.status.toUpperCase()}}</h3>
      </div>
      <img :src="require('@/assets/' + cardInformation.image)" class="col-12 col-lg-5 image"/>
      <div class="content col-12 col-lg-7">
        <div class="row mt-1 d-lg-none">
          <div class="col-12">
            <img src="@/assets/Clock.svg" class="sign col-2 p-0"/>
            <p class="duration col-9 p-0 m-0 ms-2">{{cardInformation.duration}}</p>
          </div>
        </div>
        <h3 class="title mt-2 mb-3 mb-xl-1">{{cardInformation.title}}</h3>
        <div class="row mb-2 d-none d-lg-block">
          <div class="col-12">
            <img src="@/assets/Clock.svg" class="sign col-2 p-0"/>
            <p class="duration col-9 p-0 m-0 ms-2">{{cardInformation.duration}}</p>
          </div>
        </div>
        <div class="row pb-2" v-for="content in cardInformation.content" :key="content">
          <div class="col-12">
            <img src="@/assets/checkMark.svg" class="sign col-2"/>
            <p class="inline-text col-10 ps-3 m-0">{{content}}</p>
          </div>        
        </div>
        <div class="col-12">
          <img src="@/assets/checkMark.svg" class="sign col-2"/>
          <p class="inline-text col-10 ps-3 m-0">Ближайший рейс сегодня</p>
        </div> 
        <div class="row ps-5 pb-2 mt-2">
          <input type="button" :value="time" class="voyage-time col-3 ms-1 active-custom" v-for="time in voyageTime" :key="time"/>
        </div>
        <div class="row mt-3 pb-3">
          <div class="col-5">
            <div class="row" :class="{'mt-2': !cardInformation.pierPrice}">
              <h2 class="price mb-1">
                {{cardInformation.price}}
                <img src="@/assets/ruble.png" class="ruble-sign p-0 col-1"/>
              </h2>
            </div>
            <div class="row" v-if="cardInformation.pierPrice">
              <p class="pier-price m-0">{{cardInformation.pierPrice}} р на причале</p>
            </div>
          </div>
          <input type="button" value="Подробнее" class="more col-6 active-custom"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardComponent',
  data(){
    return{
      voyageTime: this.cardInformation.voyageTime,
    }
  },
  props:{
    cardInformation: null,
  },
  created:
    function(){
      if (this.voyageTime.length > 4){
        let newTimeArr = this.voyageTime;
        newTimeArr.length = 3;
        newTimeArr[3] = 'ещё...';
        this.voyageTime = newTimeArr;
      }
    }
}
</script>

<style scoped>
.title{
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 22px;
}
.container{
  border: 0.3px solid #828282;
  border-radius: 17.6px;
}
.duration{
  color: #9E9E9E;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 20px;
  display: inline-flex;
}
.sign{
  width: 16px;
  height:16px;
  float:inline-start;
}
.content{
  padding: 0px 24px;
}
.inline-text{
  display: inline-flex;
}
.voyage-time{
  background: #D9E8FF;
  border: .3px solid #D9E8FF;
  border-radius: 11px;
  width: 4.5em;
  font-size: 14px;
  outline: none;
}
.price{
  display:inline-flex;
  font-style: normal;
  font-weight: 400;
  font-size: 30px;
  line-height: 20px;
  color: #000000;
}
.ruble-sign{
  height:22px;
  width: 18px;
}
.pier-price{
  font-style: normal;
  font-weight: 400;
  font-size: 10px;
  line-height: 20px;
  color: #000000;
}
.more{
  background: #FED74B;
  border: 0.5px solid #CBA500;
  border-radius: 20px;
  height: 44px;
  margin: auto, 0px;
  outline: none;
}
.active-custom:active{
  border: .3px solid #000000;
  opacity: .7;
}
.status-block{
  background-color: #FED74B;
  z-index:99;
  position: absolute;
  width: 180px;
  box-shadow: 3px 3px 10px #000000; 
}
.status-block h3{
  font-style: normal;
  font-weight: 600;
  font-size: 16px;
  line-height: 20px;
  color: #323232;
}
.image{
  border-radius: 21px 21px 0px 0px;
  z-index: 9;
}
@media screen and (min-width: 992px) {
  .active-custom:hover{
    border: 0.3px solid #000000;
  }
  .image{
    border-radius: 0px;
    border-radius: 21px 0px 0px 21px;
  }
}
</style>
