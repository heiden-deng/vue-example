<template>
    <div>
        <BaseInputText
            v-model="newTodoText"
            placeholder="New todo"
            @keydown.enter="addTodo"
            ></BaseInputText>
        <ul v-if="todos.length">
            <TodoListItem
                v-for="todo in todos"
                :key="todo.id"
                v-bind:todo="todo"
                v-on:remove="removeTodo"
                ></TodoListItem>
        </ul>
        <p v-else>
            Nothing left in the list. Add a new todo in the input above.
        </p>
    </div>
</template>

<script>
    import BaseInputText from "./BaseInputText"
    import TodoListItem from "./TodoListItem"
    let nextTodoId = 1
    export default {
        components:{
            BaseInputText,TodoListItem
        },
        data: function(){
            return {
                newTodoText:'',
                todos : [
                    {
                        id: nextTodoId++,
                        text: 'Learn Vue'
                    },
                    {
                        id: nextTodoId++,
                        text: 'Learn about single-file components'
                    },
                    {
                        id: nextTodoId++,
                        text: 'Fall in love'
                    }
                ]
            }
        },
        methods: {
            addTodo: function(){
                const trimmedText = this.newTodoText.trim()
                if (trimmedText){
                    this.todos.push({
                        id: nextTodoId++,
                        text: trimmedText
                    })
                    this.newTodoText = ''
                }
            },
            removeTodo: function(idToRemove){
                this.todos = this.todos.filter(todo => {
                    return todo.id !== idToRemove
                })
            }
        }
    }


</script>