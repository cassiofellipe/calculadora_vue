<script setup>
  import {ref} from 'vue'
  const calculateValue = ref('')
  const calculateElement = ref(['C','*','/','-','7','8','9','+','4','5','6','%','1','2','3', '=','0','.'])
  const operator = ref(null)
  const preValeu = ref('')

  function action(ele){

    if(!isNaN(ele) || ele === ".") {
      this.calculateValue += ele + ''
    }

    if(ele === "C"){
      this.calculateValue = ''
    }

    if (ele === '%') {
      this.calculateValue = this.calculateValue / 100;
    }

    if(['*','/','-','+'].includes(ele)){
      this.operator = ele
      this.preValeu = this.calculateValue
      this.calculateValue = ''
    }

    if(ele === '='){
      this.calculateValue = eval(
        this.preValeu + this.operator + this.calculateValue
      )
      this.operator = null
      this.preValeu = ''
    }

  }

  
</script>

<template>
  <div class="bg-[#234] max-w-[450px] p-6 mx-auto mt-5 shadow-md shadow-slate-900">

    <div class="w-full bg-slate-800 p-3 shadow-md shadow-slate-900 text-right text-white font-bold text-xl">
    {{ calculateValue || 0 }}
    </div>

    <div class="grid grid-cols-4 gap-3 mt-5">
      <div class="" v-for="ele in calculateElement" :key="ele">
        <div class="p-5 bg-slate-800 hover:bg-slate-950 transition-all duration-200 text-white
        text-center font-medium text-md cursor-pointer"
        :class="{'bg-green-500 hover:bg-green-600' : ['C','*','/','-','%','+','='].includes(ele)}"
        @click="action(ele)"
        >
          {{ ele }}
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped> 

</style>
