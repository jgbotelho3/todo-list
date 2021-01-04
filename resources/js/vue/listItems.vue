<template>
<div class="listView">
    <div v-for="(item, index) in items" :key="index" class="item">
        <list-item :item="item" v-on:itemchanged="$emit('reloadList')"/>
    </div>
</div>
</template>

<script>
import listItem from "./listItem";
export default {
    props: ['items'],
    components: {listItem}
}
</script>

<style scoped>
    .listView{
        display: flex;
        flex-direction: column;
        width: 100%;
        height: 100vh;
        margin-top: 2rem;
    }

    .item{
        padding: 1rem;
        width: 100%;
    }
</style>

