<template>
    <h1 class="mt-40 text-white text-center text-5xl mb-8 font-semibold">Todo App</h1>
    <div class="max-w-[425px] mx-auto px-4">
        <input type="text" v-model="items" class="inline-block w-full p-3 outline-none text-[#060921]"
            placeholder="Add Item" @keyup.enter="addItem">
        <i class="fa-solid fa-plus ml-[-28px] text-xl text-[#060921] cursor-pointer" @click="addItem"></i>
    </div>
    <ul class="max-w-[425px] mx-auto mt-8 px-4">
        <li class="bg-[#5535be] p-2 flex justify-between items-center mb-2" v-for="x in todos"><span
                class="text-white text-lg font-semibold">{{ x }}</span> <i
                class="fa-solid fa-trash text-white text-xl cursor-pointer" @click="removeItem(todos.indexOf(x))"></i>
        </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            todos: [],
            items: ""
        }
    },
    methods: {
        addItem() {
            if (this.items.trim() !== "") {
                this.todos.push(this.items.trim());
                this.items = "";
                this.toLocalStorage();
            }
        },
        toLocalStorage() {
            localStorage.setItem("todo", JSON.stringify(this.todos))
        },
        removeItem(index) {
            this.todos.splice(index, 1);
            this.toLocalStorage();
        },
        getLocalStorage() {
            const saveData = localStorage.getItem("todo");
            if (saveData) {
                this.todos = JSON.parse(saveData)
            }
        }
    },
    mounted() {
        this.getLocalStorage();
    }
}
</script>
