<template>
  <div>
<h1>
 <CompHeader :totalIncome="state.totalIncome" />
 <CompForm @add-income="AddIncome" />
</h1>
<section>
  <IncomeList :state="state" @remove-item="RemoveItem" />
</section>
</div>
</template>

<script>
import {reactive, computed} from 'vue';
import CompHeader from "./components/CompHeader"
import CompForm from "./components/CompForm.vue"
import IncomeList from './components/IncomeList.vue';
export default{
  components:{
    CompHeader,
    CompForm,
    IncomeList
  },
  setup(){
    const state = reactive({
      income:[
       
      ],
      totalIncome:computed(()=>{
        let temp = 0;
        const sumWithInitial = state.income.reduce(
          (accumulator, currentValue) => accumulator + currentValue.value,
          temp);
        return sumWithInitial;
      }),
      sortedIncome:computed(()=>{
        let temp = [];
        const arr = [...state.income];
        temp = arr.sort((a,b)=>{return b.date-a.date;});
      
        return temp;
      })
    })


    const AddIncome =(data)=>{
      let d = data.date.split("-");
      let newD = new Date(d[0],d[1],d[2]);

      console.log("in main: ",data);
      state.income = [...state.income,{
        id: Date.now(),
        value:data.value,
        desc:data.desc,
        date: newD.getTime(),

      }];
      console.log(state.income);
    }
    const RemoveItem =(id)=>{
      let arr = [...state.income];
      arr = arr.filter(s=>s.id!==id);

      state.income = arr;

    }
    return{
      CompHeader,
      state,
      AddIncome,
      RemoveItem
    }
  }
}
</script>

<style>
 *{
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Courier New', Courier, monospace;
 }

 body{
  background-color: #eee;
 }
</style>
