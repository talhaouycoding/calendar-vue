<template>
  <div class="m-0">
    <h1 class="text-2xl my-2 text-center">Calendar vue</h1>
    <section class="mx-3 flex justify-between">
      <h2 class="font-bold">{{currentMonthName}}</h2>
      <h2 class="font-bold">{{currentYear}}</h2>
    </section>
  <section class="flex">
    <p class="text-center my-2"  style="width:14.28%;"  v-for="day in days" :key="day">{{ day }}</p>
  </section>
    <section class="flex flex-wrap">
    <p class="text-center" style="width:14.28%;" v-for="num in startDay()" :key="num"></p>
  
    <p class="text-center" style="width:14.28%;" v-for="num in daysInMonth()" 
    :key="num"
    :class="currentDayClass(num)"

    >{{num}}</p>
  </section>
  <section class="flex justify-between">
    <button class="px-2 border rounded" @click="prev"><i class="fas fa-chevron-left"></i></button>
    <button class="px-2 border rounded" @click="next"><i class="fas fa-chevron-right"></i></button>
  </section>
  </div>
</template>

<script>
export default {
  data(){
    return {
      currentDate: new Date().getUTCDate(),
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      days: ['Sun','Mon','Tue','Wed','Thu','Fri','Sat']
    }
  },
  methods:{
    daysInMonth(){
      return new Date(this.currentYear,this.currentMonth+1,0).getDate()
    },
    startDay(){
      return new Date(this.currentYear,this.currentMonth,1).getDay()
    },
    next(){
      if(this.currentMonth === 11){
        this.currentMonth = 0
        this.currentYear++
      }else{
         this.currentMonth++
      }
      
    },
    prev(){
      if(this.currentMonth === 0){
        this.currentMonth = 11
        this.currentYear--
      }else{
        this.currentMonth--
      }
      
    },
    currentDayClass(day){
      const calendarFullDate = new Date(this.currentYear,this.currentMonth,day).toDateString()
      const currentFullDate = new Date().toDateString()
      return calendarFullDate === currentFullDate ? 'bg-yellow-600': ''
    }
  },
  computed:{
    currentMonthName(){
      return  new Date(this.currentYear,this.currentMonth).toLocaleString("default",{month: "long"})
    }
  }
}
</script>

<style>

</style>