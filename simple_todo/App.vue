<template>
    <div id="app">
        <h1 v-html="title"></h1>
        <input v-model="newItem" v-on:keyup.enter="addNew"></input>
        <ul>
            <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinnish(item)">
                {{ item.label }}
            </li>
        </ul>
    </div>
</template>

<script>
import Store from "./store"
export default {
    data: function() {
        return {
            title: "this is a todolist",
            items: Store.fetch(),
            newItem: ""
        }
    },
    watch : {
        items: {
            handler: function(items) {
                console.log(items)
                Store.save(items)
            },
            deep: true
        }
    },
    methods: {
        toggleFinnish: function(item) {
            console.log("is finished:", item.isFinished)
            item.isFinished = !item.isFinished
        },
        addNew: function() {
            this.items.push({
                label: this.newItem,
                isFinished: false
            })
            this.newItem = ""
        }
    }
}
</script>

<style>
.finished {
    text-decoration: line-through;
}
li {
    list-style:none,
}

</style>
