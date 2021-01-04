<template>
    <div class="addItemContainer">
        <input type="text" class="inputForm" aria-label="input Item" aria-describedby="input Item" placeholder="Type your todo item" v-model="item.name">
        <font-awesome-icon icon="plus-square" :class="[item.name ? 'active' : 'inactive', 'plus']" @click="addItem()" />
    </div>

</template>

<script>
export default {
    data: function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods:{
        addItem() {
            if(this.item.name === ''){
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            }).then(response => {
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadList');
                }
            }).catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.addItemContainer{
    display: flex;
}
.inputForm{
    min-width: 100%;
    height: 2rem;
    border: none;
    border-bottom: 1px solid #ccc;
    outline: none;
    color: #5C5D67;
}

.plus{
    font-size: 2rem;
    margin-left: 1rem;
    cursor: pointer;
}
.active{
    color: #3E885B;
}

.inactive{
    color: #5C5D67;
}
</style>

