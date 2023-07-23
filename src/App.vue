<template>
  <MainHeder />
  <mainCalculator />
  <hebcalCalendar />
  <FullCalendar />
  <p>{{ events }}</p>
</template>

<script>
import MainHeder from "./components/MainHeder.vue";
import mainCalculator from "./components/mainCalculator.vue";
// import hebcalCalendar from "./components/hebcalCalendar.vue";
// import FullCalendar from "@fullcalendar/vue";
// import { HebrewCalendar, HDate, Location, Event } from '@hebcal/core';

export default {
  name: "App",
  components: {
    MainHeder: MainHeder,
    mainCalculator: mainCalculator,
    // hebcalCalendar: hebcalCalendar,
    // FullCalendar: FullCalendar,
  },
  methods: {

  },

  // נסיון לוח שנה
  // data() {
  //   let options = {
  //     year: 2022,
  //     isHebrewYear: false,
  //     candlelighting: true,
  //     location: Location.lookup('Jerusalem'),
  //     sedrot: true,
  //     omer: true,
  //   };
  //   const events = HebrewCalendar.calendar(options);


  // }

};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
