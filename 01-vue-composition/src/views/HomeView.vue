<template>
  <div class="home">
  <h1>{{ title }}</h1>
  <h3>{{ counterData.myTitle }}:</h3>
    <div>
      <button class="btn" @click="dec(2, $event)">--</button>
      <button class="btn" @click="dec(1, $event)">-</button>
      <span class="counter">{{ counterData.counter }}</span>
      <button class="btn" @click="inc(1, $event)">+</button>
      <button class="btn" @click="inc(2, $event)">++</button>
    </div>

    <div>
      <h2 ref="oddEvenValue">this is an {{ oddOrEven }} number</h2>
      <input v-model="counterData.myTitle" type="text">
    </div>
  </div>
</template>
<script setup>
/*
  imports
*/
  import { ref, reactive, computed, watch, onMounted } from 'vue'

  const title = "My App"

  const counterData = reactive({
    counter:0,
    myTitle:'My Title',
  })

  const oddEvenValue = ref(null)

  onMounted(() => {
    console.log(oddEvenValue.value.offsetWidth)
  })
  watch(() => oddEvenValue.value.offsetWidth, (newVal, oldVal) => {
    console.log(newVal)
  })


  // for ref and none-reactive data we can use watch like..
  // watch(counter,(newVal, oldVal) => {}), but for reactive data:
  watch(() => counterData.counter, (newVal, oldVal) => {
    console.log(`new value is: ${newVal} and old value is: ${oldVal}`)
  })
  watch(() => counterData.myTitle, (NV, OV) => {
    console.log(NV)
  })


  const oddOrEven = computed(() => {
    if(counterData.counter % 2 === 0){
      return "odd"
    }else{
      return 'even'
    }
  })

  const inc = (amount, e) => {
    counterData.counter += amount
    // console.log(e)
  }

  const dec = (amount, e) => {
    counterData.counter -= amount
    // console.log(e)
  }
</script>
<style>
  .home{
    text-align: center;
    padding: 30px;
  }
  .btn, .counter {
    margin: 0 10px;
    font-size: 2rem;
  }
  .btn{
    min-width: 60px;
    min-height: 40px;
  }
</style>
<!--
<script>
import { ref } from 'vue';
  export default {
    setup(){
      const counter = ref(0)

      const inc = () => {
        counter.value++
      }

      const dec = () => {
        counter.value--
      }


      return{
        counter,
        inc,
        dec,
      }
    }
  }
</script>
-->
<!--

<script>
  export default {
    data(){
      return{
        
      }
    },
    methods:{
    },
    mounted(){
      console.log('mounted')
    },
    created(){
      console.log('created')
    },
    unmounted(){
      console.log('unmounted')
    },
    destroyed() {
      alert('destroyed')
    },
    beforeMount(){
      console.log('beforeMount')
    },
    beforeCreate(){
      console.log('beforeCreate')
    },
  }
</script>
-->

