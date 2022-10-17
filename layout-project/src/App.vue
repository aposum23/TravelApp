<template>
  <div class="container mt-3">
    <CardComponent class="card" :cardInformation="information" v-for="information in cards" :key="information.id"/>
  </div>
</template>

<script>
import CardComponent from './components/CardComponent.vue'

export default {
  name: 'App',
  components: {
    CardComponent,
  },
  data(){
    return{
      cards: [{
        id: 1,
        status: 'круглый год',
        image: 'stPet.png',
        title: 'АКЦИЯ - Обзорная экскурсия по рекам и каналам с остановками Hop on Hop Off 2019',
        content: ['Билет на целый день', 
        'Неограниченное число катаний', 
        '6 остановок у главных достопримечательностей'],
        voyageTime: ['12:00', '12:00', '12:00', '12:00'],
        duration: '2 часа',
        price: 900,
        pierPrice: 1200},
        {
        id: 2,
        status: 'Новинка',
        image: 'stPet.png',
        title: 'АКЦИЯ - Обзорная экскурсия по рекам и каналам с остановками Hop on Hop Off 2019',
        content: ['Билет на целый день', 
        'Неограниченное число катаний', 
        '6 остановок у главных достопримечательностей'],
        voyageTime: ['12:00', '12:00', '12:00', '12:00'],
        duration: '2 часа',
        price: 900,
        pierPrice: null},
        {
        id: 3,
        image: 'stPet.png',
        title: 'АКЦИЯ - Обзорная экскурсия по рекам и каналам с остановками Hop on Hop Off 2019',
        content: ['Билет на целый день', 
        'Неограниченное число катаний', 
        '6 остановок у главных достопримечательностей'],
        voyageTime: ['12:00', '12:00', '12:00', '12:00', '12:00'],
        duration: '2 часа',
        price: 900,
        pierPrice: 1200}],
    }
  }
}
</script>

<style scoped>
.card{
  margin-bottom: 1.9em;
}
</style>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap');

#app {
  font-family: 'Open Sans';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
