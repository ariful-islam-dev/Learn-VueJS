<template>
    <div>
        <div>
            <h1>{{ message }}</h1>
            <p>Count is : {{ counter.count }}</p>
            <button v-on:click="increment">Increment</button>
            <button @click="decrement">decrement</button>
        </div>
        <hr style="margin: 10px 0px ;">
        <div>
            <input v-model="text" @input="onInput" placeholder="Try Here">
            <p>{{ text }}</p>
        </div>
        <hr style="margin: 10px 0px ;">
        <div>
            <h1 v-if="awesome">Vue is awesome</h1>
            <h1 v-else>😂 Oh no</h1>
            <button v-on:click="toggle">Toggle</button>
        </div>
        <hr style="margin: 10px 0px ;">
        <div>
            <form v-on:submit.prevent="addTodo">
                <input type="text" v-model="newTodo" required placeholder="new todo">
                <button>Add Todo</button>
            </form>
            <ul>
            <li v-for="todo in todos" :key="todo.id">
                <input type="checkbox" v-model="todo.done" :class="{check}"> 
                <span :class="{done: todo.done}">{{ todo.text }}</span>
                <button @click='removeTodo(todo)' style="margin-left: 10px;"> X</button>
            </li>
        </ul>
        </div>
        <div>
            <p ref="pElementRef">Hello</p>
        </div>
        <!-- Watcher -->
        <div>
            <p v-if="!todoData"> Loading...</p>
            <pre v-else >{{ todoData }}</pre>
        </div>

        <!-- child Component -->
         <div>
            <ChildComp/>
         </div>
    </div>

</template>
<script >
import ChildComp from '@/components/ChildComp.vue';


let id = 0;

export default {
    data() {
        return {
            message: 'Hello World',
            counter: {
                count: 0
            },
            text: '',
            awesome: true,
            newTodo: '',
            todos: [
                {id: id++, text: 'Learn HTML', done: true},
                {id: id++, text: 'Learn CSS', done: true},
                {id: id++, text: 'Learn VueJS', done: false},
            ],
            todoId: 5,
            todoData: null
        }
    },
    methods: {
        increment() {
            this.counter.count++
        },

        decrement() {
            if (this.counter.count > 0) {
                this.counter.count--
            }
        },
        onInput(e) {
            this.text = e.target.value;
        },
        toggle(){
            this.awesome = !this.awesome
        },
        addTodo(){
            this.todos.push({id: id++, text: this.newTodo, done: false})
            this.newTodo = ''
        },
        removeTodo(todo){
            this.todos = this.todos.filter(t=>t !== todo)

        },

        async  fetchData(){
            this.todoData = null;
            const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${this.todoId}`);
            this.todoData = await res.json();
        }
    },
    mounted() {
        this.$refs.pElementRef.textContent = 'mounted!',
        this.fetchData();
    },
    components:{
        ChildComp
    }
}
</script>
<style>
    .done{
        text-decoration: line-through;
    };
    .check{
        margin-right: 10px
    }
</style>