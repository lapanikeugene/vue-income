<template>
    <div>
        <div class="income-list">
            <IncomeItem v-for="data in state.sortedIncome" :key="data.id" :income="data" @remove-item="RemoveItem" />
        </div>
    </div>
</template>

<script>
    import IncomeItem from './IncomeItem.vue';
    export default {
        props:{
            state:Object,
        }, 
        setup(_, {emit}){
            const RemoveItem =(id)=>{
                emit('remove-item',id)
            }

            return {RemoveItem}
        } ,
        components:{
            IncomeItem,
        }
    }
</script>

<style  scoped>
.income-list{
    margin-top:10px;
    padding:15px;
}
</style>