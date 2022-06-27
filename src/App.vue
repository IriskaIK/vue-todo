<template>
  <div id="app">
    <header-menu @showInfo='showInfo' ></header-menu>
    <info-card v-if="isInfoCard" @hideInfo='hideInfo'></info-card>
    <div v-else class="td_card">
      <div class="title">ToDo list</div>

    <div class="td_inner">
      <div class="task_list">
        <task-component
          v-for="(task, index) in tasks"
          :task="task"
          :key="task.id"
          @deleteTask="removeTask(index)"
          @returnTask="returnTask(index)"
          @completeTask="completeThisTask(index)"
        ></task-component>
        <div v-if="isInput" class="input_task">
          <input
            class="input_text"
            type="text"
            @click="checkWarning"
            v-model="text"
            @keyup.enter="saveTask"
          />
          <div class="date">{{ date }}</div>
          <i class="fa-solid fa-floppy-disk save_task" @click="saveTask"></i>
        </div>
        <div v-else class="add_task_btn" @click="showInput">
          <i class="fa-solid fa-plus"></i>
          Add new task
        </div>
      </div>
    </div>
    </div>
    
  </div>
</template>

<script>
import TaskComponent from "./components/task.vue";
import HeaderMenu from "./components/headerMenu.vue";
import infoCard from './components/info.vue'
export default {
  name: "App",
  components: {
    TaskComponent,
    HeaderMenu,
    infoCard
  },
  data() {
    return {
      tasks: [
        {
          text: "testTask",
          date: "25/06/2022",
          complete: false,
        },
        {
          text: "testTaskComplete",
          date: "25/06/2022",
          complete: true,
        },
      ],
      text: "",
      date: "",
      isInput: false,
      warned: false,
      isInfoCard: true
    };
  },
  methods: {
    getDate() {
      let today = new Date();
      let dd = String(today.getDate()).padStart(2, "0");
      let mm = String(today.getMonth() + 1).padStart(2, "0");
      let yyyy = today.getFullYear();
      today = mm + "/" + dd + "/" + yyyy;
      return today;
    },
    showInput() {
      this.isInput = true;
      this.text = "";
      this.date = this.getDate();
    },
    saveTask() {
      console.log(this.text);

      if (this.text != "") {
        this.tasks.push({
          text: this.text,
          date: this.date,
          complete: false,
        });
        this.isInput = false;
      } else {
        this.text = "Enter text";
        this.warned = true;
      }
    },
    hideInfo(){
      this.isInfoCard=false
    },
    showInfo(){
      this.isInfoCard=true
    },
    checkWarning() {
      if (this.warned) {
        this.text = "";
        this.warned = false;
      } else {
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    completeThisTask(index) {
      this.tasks[index].complete = true;
    },
    returnTask(index) {
      this.tasks[index].complete = false;
    },
    
    
  },
};
</script>

<style>
.td_inner {
  width: 600px;
  margin: 0 auto;
  border: 1px #000 solid;
  border-radius: 20px;
  /* background: url(./assets/bg.jpg) no-repeat center center fixed; */
  background-color: rgba(236, 243, 255, 0.998);
}
.title {
  max-width: max-content;
  margin: 40px auto;
  font-size: 42px;
  font-weight: 700;
}
.date {
  margin: 0 10px;
}
.save_task {
  margin: auto 0;
}
.input_task {
  height: 36px;
  border: 2px #000 solid;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 400px;
  margin: 0 auto;
}
.input_text {
  height: max-content;
  width: 300px;
  border-radius: 10px;
  border: none;
  height: 35px;
  background-color: inherit;
}
.input_text:focus {
  outline: none;
}
.add_task_btn {
  max-width: max-content;
  margin: 20px auto;
  padding: 5px;
  border: 1px #000 solid;
  border-radius: 10px;
  background-color: rgb(115, 169, 255);
  transition: all 0.2s linear;
  cursor: pointer;
}
.add_task_btn:hover {
  background-color: rgb(102, 148, 223);
  color: #fff;
}
</style>
