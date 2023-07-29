<template>
    <div>
    <div class="income-item">
            <div class="removeItem" @click="RemoveItem">X</div>
            <div class="desc">{{income.desc}}</div>
            <div class="price">{{income.value}}</div>
            <div class="date">{{formattedDate}}</div>
    </div>
    </div>
</template>

<script>

    export default {
        
        props:{
            income:Object,
        },

        setup(props,{emit}){
                const date = new Date(props.income.date);
                const day = date.getDate();
                const month = date.getMonth();
                const year = date.getFullYear();
                const formattedDate = `${day}/${month}/${year}`;
                
                const RemoveItem=()=>{
                    emit('remove-item',props.income.id)
                }
                console.log(formattedDate);
            return {formattedDate,RemoveItem};
        }
    }
</script>

<style scoped>
.income-item {
    position: relative;
    display: flex;
    padding: 15px 15px 15px 0px;
    background-color: #FFF;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto 30px;
  }

  .removeItem {
    color: #EF2D2D;
    font-weight: 600;
    font-size: 20px;
    line-height: 1;
    text-align: center;
    margin: 0 15px;
  }

  .desc {
    color: #666;
    flex: 1 1 100%;
    font-size: 20px;
  }

  .price {
    color: #666;
    min-width: 100px;
    font-size: 20px;
  }

  .date {
    color: #666;
    text-align: right;
    font-size: 20px;
  }
</style>