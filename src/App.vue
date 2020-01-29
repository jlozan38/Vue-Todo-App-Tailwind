<template>
  <div class="h-screen w-width bg-red-400 flex flex-col justify-center items-center">
    <div class="header">
      <h1 class="text-4xl">Jesus's Todo App made with Tailwind and Vue!</h1>
      <div class="form flex">
        <input v-model="newTodo" @keyup="checkAdd" class="appearance-none border w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none"
          id="newText" type="text" placeholder="Add New Todo" />
        <button id="newBtn" @click="add" class="bg-teal-400 hover:bg-blue-700 text-white font-bold py-2 px-4">
          Add
        </button>
      </div>
    </div>
    <div class="todos w-1/2 mt-8">
      <div class="pendings" v-if="totalPendings>0">
        <h3 class="text-2x1">Pendings - {{totalPendings}}:</h3>
        <ul id="pendingList">
          <li @click="moveToCompleted(pending, index)" v-for="(pending, index) in pendingList" :key="index" class="text-center p-3 bg-white mt-4 rounded shadow-lg cursor-pointer hover:bg-indigo-500">
            {{pending}}
          </li>
        </ul>
      </div>
      <div class="completed mt-8" v-if="totalCompleted>0">
        <h3 class="text-2x1">Completed - {{totalCompleted}}:</h3>
        <ul id="completedList">
          <li @click="moveToPending(completed, index)" v-for="(completed, index) in completedList" :key="index"
            class="text-center p-3 bg-white line-through text-red-500 mt-4 rounded shadow-lg cursor-pointer hover:bg-red-500 hover:text-white">
            {{completed}}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "app", 
  data() {
    return {
      newTodo: "",
      pendingList: [],
      completedList: []
    };
  }, 
  computed: {
    totalPendings() {
      return this.pendingList.length;
    },
    totalCompleted() {
      return this.completedList.length;
    }
  },
  methods: {
    add() {
      if (this.newTodo != "") {
        this.pendingList.push(this.newTodo);
        this.newTodo = "";
      } else {
        alert("Please specify the task to Add");
      }
    },
    checkAdd(event) {
      if (event.keyCode === 13) {
      event.preventDefault();
      this.add();
      }
    },
    moveToCompleted(todo, index) {
      this.completedList.push(todo);
      this.pendingList.splice(index, 1);
    },
    moveToPending(todo, index) {
      this.pendingList.push(todo);
      this.completedList.splice(index, 1);
    }
  },
};
</script>


