<template>
    <div class="container">
        <div>
            <h2>Todo List</h2>
        </div>
        <add-item v-on:reloadList="getAllItems()" />
        <list-items :items="items" v-on:reloadList="getAllItems()" />
    </div>



</template>

<script>
import addItem from "./addItem";
import listItems from "./listItems";

export default {
    components: {
        addItem,
        listItems
    },
    data: function(){
        return{
            items: []
        }
    },
    methods: {
        getAllItems(){
            axios.get('api/items').then(response => {
                this.items = response.data;
            }).catch(error => {
                console.log(error);
            })
        }
    },
    created(){
        this.getAllItems();
    }
}
</script>

<style scoped>
    .container{
        display: flex;
        width: 100%;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-color: #fafafc;
    }

    h2{
        font-size: 2rem;
    }
</style>
