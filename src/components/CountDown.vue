<template>
    <div v-if="alertMessage">
        <h1>Timer Over</h1>
    </div> 
    <div v-if="!alertMessage">
        <h1>Options API</h1>
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
    export default{
        data(){
            return {
                displayDays: 0,
                displayHours: 0,
                displayMinutes: 0,
                displaySeconds: 0,
                displayYears: 0,
                alertMessage: false
            }
        },
        computed: {
            seconds: () => 1000,
            minutes() { return this.seconds * 60},
            hours() { return this.minutes * 60},
            days() { return this.hours * 24},
            years() { return this.days * 365}
        },
        methods: {
            formatNum(num){
               return  num < 10 ? '0' + Math.floor(num) : Math.floor(num)
            },
            
            calculateTimeLeft(){
                let today = new Date()
                let futureDate = new Date(2024,10,10,15,16,10)
                let distance = futureDate.getTime() - today.getTime()
                if (distance < 0) {
                    this.alertMessage = true
                }
                let Years = distance / this.years
                let Days =(distance % this.years)/this.days
                let Hours =(distance % this.days)/this.hours
                let Minutes =(distance % this.hours)/this.minutes
                let Seconds =(distance % this.minutes)/this.seconds
                this.displayDays = this.formatNum(Days)
                this.displayHours = this.formatNum(Hours)
                this.displayMinutes = this.formatNum(Minutes)
                this.displaySeconds = this.formatNum(Seconds)
                this.displayYears = this.formatNum(Years)
            }
        },
        mounted(){
            setInterval(this.calculateTimeLeft, 1000)
        }
    }
</script>

<style>

h1{
  color: #396;
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
	background: #00BF96;
	display: inline-block;
}

#clockdiv div > span{
	padding: 15px;
	border-radius: 3px;
	background: #00816A;
	display: inline-block;
}

.smalltext{
	padding-top: 5px;
	font-size: 16px;
}
</style>