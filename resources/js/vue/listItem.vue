<template>
<div class="itemDiv">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed" class="checkbox"/>
    <span :class="[item.completed ? 'completed' : '', 'itemText']">{{item.name}}</span>
    <button @click="deleteItem()" class="trash">
        <font-awesome-icon icon="trash" />
    </button>
</div>
</template>

<script>
export default {
    props: ['item'],
    methods:{
        updateCheck(){
            axios.put(`api/item/${this.item.id}`, {
                item: this.item
            }).then(response => {
                if(response.status == 200) {
                    this.$emit('itemchanged');
                }
            }).catch(error => {
                console.log(error);
            })
        },
        deleteItem(){
            axios.delete(`api/item/${this.item.id}`).then(response => {
                if(response.status == 200) {
                    this.$emit('itemchanged');
                }
            }).catch(error => {
                console.log(error)
            })
        }
        }
    }

</script>

<style scoped>

.itemDiv{
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #ccc;
}
.checkbox{
    margin-right: 1rem;
}

.completed{
    text-decoration: line-through;
}

.itemText{
    width: 100%;
    color: #5C5D67;
}

.trash{
    border: none;
    color: #ff0000;
    outline: none;
    margin-right: 1rem;
    background-color: transparent;
    font-size: 1.5rem;
    cursor: pointer;
}
</style>


