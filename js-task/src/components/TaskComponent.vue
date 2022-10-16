<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-5">
        <label for="route">Выберите направление</label>
        <select name="route" id="route"  @change="changeDirection()" v-model="direction">
          <option value="1">из A в B</option>
          <option value="2">из B в A</option>
          <option selected value="3">из A в B и обратно в А</option>
        </select>
      </div>
    </div>
    <div class="row justify-content-center mt-2">
      <div class="col-5">
        <label for="time">Выберите время</label>
        <select name="time" id="time-a" @change="changeTimeSelect('a')" v-model="timeA">
          <option v-for="time in timesA2B" :value="time" :key="time">{{time.getHours() + ':' + (time.getMinutes() === 0 || time.getMinutes() < 10 ? '0' + time.getMinutes() : time.getMinutes())}}(из A в B)</option>
        </select>
        <select name="time" id="time-b" @change="changeTimeSelect('b')" v-model="timeB">
          <option v-for="time in timesB2A" :value="time" :key="time">{{time.getHours() + ':' + (time.getMinutes() === 0 || time.getMinutes() < 10 ? '0' + time.getMinutes() : time.getMinutes())}}(из B в A)</option>
        </select>
      </div>
    </div>
    <div class="row justify-content-center mt-2">
      <div class="col-5">
        <label for="num">Количество билетов</label>
        <input type="number" id="num" v-model="numOfTickets">
      </div>
    </div>
    <div class="row justify-content-center mt-2">
      <button class="col-3" @click="calculate()">Посчитать</button>
    </div>
    <div class="row justify-content-center mt-2 text-center">
      <p>{{result}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskComponent',
  data(){
    return{
      timesReservB: ['2021-08-21 18:30:00', '2021-08-21 18:45:00', '2021-08-21 19:00:00', '2021-08-21 19:15:00', '2021-08-21 19:35:00', '2021-08-21 21:50:00', '2021-08-21 21:55:00'],
      timesA2B: ['2021-08-21 18:00:00', '2021-08-21 18:30:00', '2021-08-21 18:45:00', '2021-08-21 19:00:00', '2021-08-21 19:15:00', '2021-08-21 21:00:00'],
      timesB2A: [],
      direction: '3',
      numOfTickets: 1,
      timeA: null,
      timeB: null,
      timeInRoad: 50,
      result: '',
    }
  },
  methods:{
    changeDirection(){
      const timeA = document.getElementById('time-a');
      const timeB = document.getElementById('time-b');
      switch (this.direction){
        case '1':
          timeA.style.display = 'inline-block';
          timeB.style.display = 'none';
          break;
        case '2':
          timeB.style.display = 'inline-block';
          timeA.style.display = 'none';
          this.timesB2A = this.timesReservB;
          break;
        case '3':
          timeA.style.display = 'inline-block';
          timeB.style.display = 'inline-block';
          this.calculateTimeArrays();
          break;
      }
    },
    changeTimeSelect(){
      if (this.direction === '3'){  
        this.calculateTimeArrays();
      }
    },
    calculateTimeArrays(){
      const times = this.timesReservB;
      this.timesB2A = [];

      for(const elem of times){
        const elemTime = new Date(elem);
        const timeA = new Date(this.timeA);
        const timeAMs = new Date(timeA.getTime() + this.timeInRoad * 60 * 1000);
        if (elemTime.getTime() > timeAMs.getTime()){
          this.timesB2A.push(elemTime);
        }
      }
    },
    calculate(){
      const timeArriveA = new Date(this.timeA.getTime() + this.timeInRoad * 60 * 1000);
      const timeArriveB = new Date(this.timeB.getTime() + this.timeInRoad * 60 * 1000);

      switch (this.direction){
        case '1':
          this.result = `Количество билетов: ${this.numOfTickets}.
          Сумма к оплате: ${this.numOfTickets * 700} рублей.
          Время в пути: ${this.timeInRoad} мин.
          Время отбытия: ${this.timeA.getHours() + ':' + (this.timeA.getMinutes() === 0 ? '0' + this.timeA.getMinutes() : this.timeA.getMinutes())}.
          Время прибытия: ${timeArriveA.getHours() + ':' + (timeArriveA.getMinutes() === 0 ? '0' + timeArriveA.getMinutes() : timeArriveA.getMinutes())}`;
          break;
        case '2':
          this.result = `Количество билетов: ${this.numOfTickets}.
          Сумма к оплате: ${this.numOfTickets * 700} рублей.
          Время в пути: ${this.timeInRoad} мин.
          Время отбытия: ${this.timeB.getHours() + ':' + (this.timeB.getMinutes() === 0 ? '0' + this.timeB.getMinutes() : this.timeB.getMinutes())}.
          Время прибытия: ${timeArriveB.getHours() + ':' + (timeArriveB.getMinutes() === 0 ? '0' + timeArriveB.getMinutes() : timeArriveB.getMinutes())}`;
          break;
        case '3':
          this.result = `Количество билетов: ${this.numOfTickets}.
          Сумма к оплате: ${this.numOfTickets * 1200} рублей.
          Время в пути: ${this.timeInRoad * 2} мин.
          Время отбытия из пункта A: ${this.timeA.getHours() + ':' + (this.timeA.getMinutes() === 0 || this.timeA.getMinutes() < 10 ? '0' + this.timeA.getMinutes() : this.timeA.getMinutes())}.
          Время прибытия в пункт B: ${timeArriveA.getHours() + ':' + (timeArriveA.getMinutes() === 0 || timeArriveB.getMinutes() < 10 ? '0' + timeArriveA.getMinutes() : timeArriveA.getMinutes())}.
          Время отбытия из пункта B: ${this.timeB.getHours() + ':' + (this.timeB.getMinutes() === 0 || this.timeB.getMinutes() < 10 ? '0' + this.timeB.getMinutes() : this.timeB.getMinutes())}.
          Время прибытия в пункт A: ${timeArriveB.getHours() + ':' + (timeArriveB.getMinutes() === 0 || timeArriveB.getMinutes() < 10 ? '0' + timeArriveB.getMinutes() : timeArriveB.getMinutes())}`;
          break;
      }
    },
    changeTimeForTimeZone(time, timeAddition){
      const currentTime = new Date(time);
      return new Date(currentTime.getTime() - (timeAddition * 60 * 1000))
    }
  },
  created:
    function(){
      const date = new Date();
      const timeZone = date.getTimezoneOffset();

      if (timeZone === -180){
        this.timesA2B = this.timesA2B.map(elem => new Date(elem));
        this.timesReservB = this.timesReservB.map(elem => new Date(elem));
      }
      else{
        const timeAddition = -180 - timeZone;
        this.timesA2B = this.timesA2B.map(elem => this.changeTimeForTimeZone(elem, timeAddition));
        this.timesReservB = this.timesReservB.map(elem => this.changeTimeForTimeZone(elem, timeAddition));
      }
      this.timesB2A = this.timesReservB;
    }
}
</script>
