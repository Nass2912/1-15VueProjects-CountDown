<template>
    <div v-if="alertMessage">
        <h1>Timer Over</h1>
    </div>
    <div v-if="!alertMessage">
        <h1>Composition API</h1>
        <div id="clockdiv">
            <div>
            <span class="years">{{displayYears}}</span>
            <div class="smalltext">Years</div>
        </div>
        <div>
            <span class="days">{{displayDays}}</span>
            <div class="smalltext">Days</div>
        </div>
        <div>
            <span class="hours">{{displayHours}}</span>
            <div class="smalltext">Hours</div>
        </div>
        <div>
            <span class="minutes">{{displayMinutes}}</span>
            <div class="smalltext">Minutes</div>
        </div>
        <div>
            <span class="seconds">{{displaySeconds}}</span>
            <div class="smalltext">Seconds</div>
        </div>
        </div>
    </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue'
export default{
    props:{
        year: Number, 
        month: Number,
        date: Number,
        hours: Number,
        minutes: Number,
        seconds: Number,
        miliseconds: Number
   },
    setup(props){
        const displayYears = ref(0)
        const displayDays = ref(0)
        const displayHours = ref(0)
        const displayMinutes = ref(0)
        const displaySeconds = ref(0)
        const alertMessage = ref(false)

        const seconds = 1000;
        const minutes = computed(()=>{
           return seconds * 60
        })
        const hours = computed(()=>{
           return minutes.value * 60
        })
        const days = computed(()=>{
           return hours.value * 24
        })
        const years = computed(()=>{
           return days.value * 365
        })

        const formatDate = (date) => {
            return date < 10 ? '0'+ Math.floor(date) : Math.floor(date)
        }

        const calculteTimePassed = () => {
            const today = new Date()
            const futureDate = new Date(props.year, props.month, props.date, props.hours, props.minutes, props.seconds, props.miliseconds)
            const distance = futureDate.getTime() - today.getTime()
            if(distance <=0){
                alertMessage.value = true
                clearInterval(calculteTimePassed)
            }
            displayYears.value = formatDate(distance/years.value)
            displayDays.value = formatDate((distance % years.value) / days.value)
            displayHours.value  = formatDate((distance % days.value) / hours.value)
            displayMinutes.value = formatDate((distance % hours.value) / minutes.value)
            displaySeconds.value = formatDate((distance % minutes.value) / seconds)
        }

        onMounted(() => {
            setInterval(() => {
                calculteTimePassed()
            }, 1000);
        })

        return { displayYears, displayDays, displayHours, displayMinutes, displaySeconds, alertMessage }
    }
}
</script>

<style scoped>

h1{
  color: #722F37;
  font-weight: 100;
  font-size: 40px;
  margin: 40px 0px 20px;
}

#clockdiv{
	font-family: sans-serif;
	color: #fff;
	display: inline-block;
	font-weight: 100;
	text-align: center;
	font-size: 30px;
}

#clockdiv > div{
	padding: 10px;
	border-radius: 3px;
	background: #ac646c;
	display: inline-block;
}

#clockdiv div > span{
	padding: 15px;
	border-radius: 3px;
	background: #722F37;
	display: inline-block;
}

.smalltext{
	padding-top: 5px;
	font-size: 16px;
}
</style>