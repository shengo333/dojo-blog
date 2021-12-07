<template>
  <div class="home">
    <h1>this is home page</h1>
    <input type="text" v-model="search">
    <p>search term - {{ search }}</p>
    <div v-for="name in matchingNames" :key="name">
      <p>{{name}}</p>
    </div>
    <button @click="handleClick">stop watching</button>

    <!-- <h2>Refs</h2>
    <p>{{ ninjaOne.name }} - {{ ninjaOne.age}}</p>
    <button @click="updateNinjaOne"> Update Ninja One</button>
    <h2>Reactive</h2>
    <p>{{ninjaTwo.name}} - {{ninjaTwo.age}}</p>
    <button @click="updateNinjaTwo"> Update Ninja two</button> -->

  </div>
</template>

<script>
import { computed, ref, watch, watchEffect } from 'vue'

export default {
  name: 'Home',
  setup(){

    const search = ref ('')
    const names = ref(['mario', 'yoshi', 'luigi', 'toad', 'bowser', 'koopa', 'peach'])

    const stopWatch = watch(search, () => {
      console.log('watch function fireeeee')
    })

    const stopEffect = watchEffect(() => {
      console.log('watch effect fireee', search.value)
    })
    
    const matchingNames = computed (() =>  {
      return names.value.filter ((name) => name.includes(search.value))
    }) 

    const handleClick = () => {
      stopWatch()
      stopEffect()
    }

    return { names, search, matchingNames, handleClick }

    //const p = ref(null)

    // const ninjaOne = ref({ name: 'mario', age: 30 })
    // const ninjaTwo = reactive({ name: 'luigi', age: 35})

    // const updateNinjaOne = () => {
    //   ninjaOne.value.age = 40
    // }
    // const updateNinjaTwo = () => {
    //   ninjaTwo.age = 45
    // }
    // const name = ref ('mario ')
    // const age = ref (30)
    
    // const handleClick = () => {
    //   name.value = 'luigi'
    //   age.value = 35


      // console.log(p, p.value)
      // p.value.classList.add('test')
      // p.value.textContent = 'hello jimi'

    //return { ninjaOne, updateNinjaOne, ninjaTwo, updateNinjaTwo}
  
  }
}
</script>
