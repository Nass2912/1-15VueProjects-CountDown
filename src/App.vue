<template>
  <div class="spacer"/>
    <CountDown/>
  <div class="spacer"/>
    <CountDownComposition
    year="2024"
    month="10"
    date="10"
    hours="10"
    minutes="10"
    seconds="10"
    miliseconds="10"
    />
</template>

<script>
import CountDown from './components/CountDown.vue'
import CountDownComposition from './components/CountDownComposition.vue';
export default {
  components: {
    CountDown,
    CountDownComposition
  }
}
</script>

<style>
body{
	text-align: center;
  font-family: sans-serif;
  font-weight: 100;
}

.spacer{
  margin: 4rem;
}
</style>