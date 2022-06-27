<template>
  <div class="info">
    <div class="title_info">{{ content[contentId].title }}</div>
    <img :src="content[contentId].src" class="img" />
    <div class="text_info">{{ content[contentId].text }}</div>
    <div class="control_btns">
      <div v-if="content[contentId].isComplete" @click="$emit('hideInfo')" class="complete_btn info_btn_control">
        Complete
      </div>
      <div v-else>
        <div class="next_btn info_btn_control" @click="incrementId">Next</div>
        <div class="skip_btn info_btn_control" @click="$emit('hideInfo')">Skip</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      content: [
        {
          text: '1) You can create a task using the "add task" button \n 2) You can mark the task as completed using the "check" button \n3) You can delete a task using the "minus" button',
          title: "How to",
          isComplete: false,
          src: require(`@/assets/img/info1.webp`),
        },
        {
          text: "You can revert a completed task to an uncompleted one",
          title: "Somer more info",
          isComplete: true,
          src: require("@/assets/img/info2.webp"),
        },
      ],
      contentId: 0,
    };
  },
  methods: {
    incrementId() {
      this.contentId++;
    },
  },
};
</script>

<style>
.title_info {
  margin: 10px auto;
  font-size: 42px;
  font-weight: 700;
  text-align: center;
}
.info {
  background-color: #fff;

  border: 1px #000 solid;
  border-radius: 20px;
  width: 600px;
  margin: 0 auto;
  margin-top: 30px;
}
.text_info {
  text-align: center;
}

.control_btns {
  font-size: 20px;
  font-weight: 600;
  margin: 10px;
  display: flex;
  justify-content: center;
}
.info_btn_control{
    transition: color 0.25s linear;


}
.img{
    width: 600px;
    height: auto;
    
}
.info_btn_control:after{
  display:block;
  content: '';
  border-bottom: solid 2px #000;  
  transform: scaleX(0);  
  transition: transform 250ms ease-in-out;
}
.info_btn_control:hover{
    cursor: pointer;
    color: #000;
    
}
.info_btn_control:hover:after{
    transform: scaleX(1);
}
</style>