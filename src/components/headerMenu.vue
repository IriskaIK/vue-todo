<template>
  <header class="header">
    <div class="info_btn menu_btn" @click="$emit('showInfo')"> 
      <p>Get Started</p>
    </div>
    <div class="styles_btn menu_btn">
      <p>Change style</p>
    </div>
    <div class="links_btn menu_btn">
      <p>Links</p>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {},
};
</script>

<style>
.header {
  display: flex;
  background-color: rgb(115, 169, 255);
  justify-content: center;
  align-items: center;
  height: 60px;
  width: 100%;
  color: #fff;
}

.menu_btn {
  height: 100%;
  width: 100px;
  transition: all 0.2s;
  text-align: center;
  cursor: pointer;
}
.menu_btn:hover {
  background-color: rgb(102, 148, 223);
}
</style>