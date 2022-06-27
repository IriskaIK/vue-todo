<template>
  <div class="task" v-bind:class="{ complete: task.complete }">
    <div v-bind:class="{ complete_text: task.complete }" class="text">
      {{ task.text }}
    </div>
    <div class="task_control">
      <div v-bind:class="{ complete_text: task.complete }" class="date">
        {{ task.date }}
      </div>
      <i
        class="fa-solid fa-circle-minus delete_btn"
        @click="$emit('deleteTask')"
      ></i>
      <i
        v-if="!task.complete"
        class="fa-solid fa-circle-check check_btn"
        @click="$emit('completeTask')"
      ></i>
      <i
        v-else
        class="fa-solid fa-arrows-rotate return_btn"
        @click="$emit('returnTask')"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["task"],
};
</script>

<style>
.complete {
  background-color: rgb(147, 144, 144);
  opacity: 0.5;
}
.complete_text {
  text-decoration: line-through;
}

.task_control {
  display: flex;
  align-items: center;
}
.return_btn:hover {
  opacity: 1;
  color: rgb(10, 50, 209);
  cursor: pointer;
}
.task {
  transition: all 0.2s;
  padding: 5px;
  margin: 20px auto;
  width: 400px;
  display: flex;
  justify-content: space-between;
  border: 1px #000 solid;
  border-radius: 10px;
  align-items: center;
  transition: all 0.2s;
}
.task:hover {
  box-shadow: 10px 5px 5px rgb(127, 125, 125);
}
.text {
  overflow-x: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.task_conrol {
  display: flex;
  align-items: center;
}
.delete_btn {
  margin: 0 10px;
  cursor: pointer;
  opacity: 1;
}
.delete_btn:hover {
  color: rgb(164, 6, 51);
}
.check_btn:hover {
  color: rgb(77, 186, 8);
  cursor: pointer;
}
</style>