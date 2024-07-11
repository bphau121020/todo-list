
<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = "";
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    removeCompletedTasks() {
      this.tasks = this.tasks.filter(task => !task.completed);
    },
  },
};
</script>

<template>
  <div class="container">
    <section class="section-todo">
      <div class="wrapper">
        <div class="todo-inner">
          <h1 class="todo-title">Todo List</h1>
          <div class="todo-input">
            <input class="input-task" type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Enter a new task" />
            <button class="input-button" @click="addTask">Add</button>
          </div>
          <ul class="todo-list">
            <li class="list-item" v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
              <input class="item-complete" type="checkbox" v-model="task.completed" />
              <span class="item-text">{{ task.name }}</span>
              <button class="item-button" @click="removeTask(index)">Remove</button>
            </li>
          </ul>
          <button class="todo-delete-all" @click="removeCompletedTasks">Remove Select Tasks</button>
        </div>
      </div>
    </section>
  </div>
</template>
  <style scoped>
  .section-todo {
    height: 100vh;
    position: relative;
  }
  
  .section-todo::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url("../assets/bg_capture.jpg") top center / cover no-repeat;
    filter: blur(5px);
    opacity: 1;
    z-index: -1;
  }
  
  .todo-inner {
    margin: 0 auto;
    text-align: center;
    border: 1px solid #333;
    border-radius: .04rem;
    padding: .1rem .2rem;
    background-color: #fff;
  }

  .todo-input {
    display: flex;
    justify-content: center;
  }
  
  .todo-title {
    text-decoration: underline;
    text-underline-offset: .03rem;
  }
  
  .todo-list {
    list-style-type: none;
    padding: 0;
  }
  
  .todo-input .input-task {
    border: 1px solid #000;
    border-radius: .03rem;
    padding: .05rem .1rem;
    font-size: .16rem;
  }
  
  .todo-input .input-button {
    border-radius: 1px solid #f5f5f5;
  }

  li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: .05rem 0;
  }

  li.completed span {
    text-decoration: line-through;
    opacity: 0.5;
  }
  
  button {
    cursor: pointer;
    background-color: #3fa2f6;
    color: #fff;
    border-radius: .03rem;
    padding: .1rem .15rem;
    transition: opacity .3s ease;
  }
  
  button:hover {
    opacity: .8;
    transition: opacity .3s ease;
  }
  
  .item-text {
    display: inline-block;
    text-align: left;
  }
  
  .list-item {
    border-bottom: 1px solid #333;
  }
  
  .list-item:last-child {
    border-bottom: 0;
  }
  
  .list-item input {
    border: 1px solid #000;
    outline: none;
    position: relative;
    width: .14rem;
    height: .14rem;
  }
  
  .list-item.completed input::before{
    position: absolute;
    content: '';
    width: .07rem;
    height: .07rem;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #000;
  }

@media print, (min-width: 768px) {
  .section-todo {
    padding: 100px 0;
  }

  .todo-inner {
    max-width: 600px;
    min-height: 400px;
  }
  
  .todo-title {
    font-size: .34rem;
  }
  
  .todo-input {
    margin-bottom: 20px;
  }
  
  .todo-input input {
    width: 200px;
    padding: 5px;
    margin-right: 20px;
  }
  
  .todo-input .input-task {
    min-width: 2.5rem;
  }
  
  .item-text {
    width: 400px;
    font-size: .18rem;
    letter-spacing: .1em;
  }
  
  .list-item input {
    cursor: pointer;
  }
}

@media only screen and (max-width: 767.98px) {
  .section-todo {
    padding: .6rem 0;
    
  }
  
  .todo-inner {
    width: 100%;
  }
  
  .todo-input {
    margin-bottom: .28rem;
  }
  
  .input-task {
    margin-right: .2rem;
  }
  
  .item-text {
    width: 1.8rem;
  }
}

</style>
