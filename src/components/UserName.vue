<template>
    <div ref="box" class="max-w-sm bg-slate-200 p-5 mx-auto mb-5">
        <input @keyup.enter="addItem" ref="inp" v-model="newItem" type="text" placeholder="Add Item"
            class="px-4 py-[10px] text-lg outline-none">
        <button v-on:click="addItem" class="px-4 bg-gray-600 py-[10px] ml-2 text-white text-lg">Add</button>
    </div>
    <ul class="max-w-sm mx-auto">
        <li class="" v-for="x in todo">
            <span class="text-xl font-semibold mr-2">{{ todo.indexOf(x) + 1 }}</span>
            <span class="text-xl font-semibold">{{ x }}</span>
            <button v-on:click="removeItem(todo.length - 1)" class="ml-2 text-red-500 text-lg font-medium">X</button>
        </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            newItem: "",
            todo: []
        }
    },
    methods: {
        addItem: function () {
            let value = this.newItem.trim();
            if (value) {
                this.todo.push(this.newItem);
                localStorage.setItem(this.todo.indexOf(value) + 1, value)
                this.newItem = "";
                this.$refs.inp.classList.remove("border-2");
                this.$refs.inp.classList.remove("border-red-500");
                this.$refs.box.classList.remove("bg-red-200");
            } else {
                this.$refs.inp.classList.add("border-2");
                this.$refs.inp.classList.add("border-red-500");
                this.$refs.box.classList.add("bg-red-200");
            }
            console.log(this.todo)
        },
        removeItem: function (index) {
            this.todo.splice(index, 1);
        }
    }
}
</script>
