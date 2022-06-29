<template>
  <div id="app">
    <header-menu @showInfo="showInfo" @changeColorAdd='changeAddColor' @setStartColor='setStartColor' @changeSecondColor='changeSecondColor' @changeText='changeTextColor'></header-menu>
    <info-card v-if="isInfoCard" @hideInfo="hideInfo"></info-card>
    <div v-else class="td_card">
      <div class="title">ToDo list</div>

      <div class="td_inner" :style="{backgroundColor:this.secondColor}">
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
          <div :style="{backgroundColor:this.firstColor, color:this.textColor}" v-else class="add_task_btn" @click="showInput">
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
import infoCard from "./components/info.vue";
export default {
  name: "App",
  components: {
    TaskComponent,
    HeaderMenu,
    infoCard,
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
      isInfoCard: true,
      firstColor:'#73a9ff',
      secondColor:'#ecf3ff',
      textColor:'#000',
      MainfirstColor: "#73a9ff",
      MainsecondColor: "#ecf3ff",
      MaintextColor: "#fff",
    };
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      try {
        this.tasks = JSON.parse(localStorage.getItem("tasks"));
      } catch (e) {
        localStorage.removeItem("tasks");
      }
    }
    if (localStorage.getItem("info") == 'was') {
      this.isInfoCard = false
    }
  },
  methods: {
    checkInfo(){
      localStorage.setItem('info', 'was')
    },
    addToStorage() {
      if (!this.text) {
        return;
      }
      this.updateStorage();
    },
    updateStorage() {
      const parsed = JSON.stringify(this.tasks);
      localStorage.setItem("tasks", parsed);
    },
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
        this.addToStorage();
        this.isInput = false;
      } else {
        this.text = "Enter text";
        this.warned = true;
      }
    },
    hideInfo() {
      this.isInfoCard = false;
      this.checkInfo()
    },
    showInfo() {
      this.isInfoCard = true;

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
      this.updateStorage();
    },
    completeThisTask(index) {
      this.tasks[index].complete = true;
      this.updateStorage()
    },
    returnTask(index) {
      this.tasks[index].complete = false;
      this.updateStorage()
    },
    changeAddColor(data){
      this.firstColor = data
    },
    changeSecondColor(data){
      this.secondColor = data
    },
    changeTextColor(data){
      this.textColor = data
    },
    setStartColor(){
      this.firstColor = this.MainfirstColor
      this.secondColor = this.MainsecondColor
      this.textColor = this.MaintextColor
    }
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
  color: #fff;
}
.add_task_btn:hover {
  box-shadow: 3px 3px 3px rgb(127, 125, 125);
}
</style>
