<template>
  <header
    :style="{ backgroundColor: this.firstColor, color: this.textColor }"
    class="header"
  >
    <div class="info_btn menu_btn" @click="$emit('showInfo')">
      <p>Get Started</p>
    </div>
    <div class="styles_btn menu_btn dropdown">
      <p>Change style</p>
      <div class="dropdown-content">
        <div class="menu-item color-item" @click="isColorPicker = true">
          <p>Choose color</p>
          <div v-if="isColorPicker" class="color-picker">
            <div class="cl_item">
              <p>First color</p>
              <input v-model="firstColor" type="color" name="" id="" />
            </div>
            <div class="cl_item">
              <p>Second color</p>
              <input v-model="secondColor" type="color" name="" id="" />
            </div>
            <div class="cl_item">
              <p>Text color</p>
              <input v-model="textColor" type="color" name="" id="" />
            </div>
            <div class="cl_item">
              <button @click.stop="isColorPicker = false">Cancel</button>
              <button @click.stop="setMainColor">Reset</button>
            </div>
          </div>
        </div>
        <div class="menu-item set-bg" @click="setBg">
          <p>Set background</p>
          <div v-if="isBgSet">
            <div  class="link_inner">
              <div class="link-holder">Paste a link</div>
              <input v-model="link" class="link_input" type="text" />
            </div>
            <div class="bg-btns">
              <button @click="useBg" class="set-bg-btn">Set</button>
              <button class="set-bg-btn" @click="cancelBg">Cancel</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="links_btn menu_btn dropdown">
      <p>Links</p>
      <div class="dropdown-content">
        <a class="menu-item" target="_blank" href="https://github.com/IriskaIK"
          >GitHub</a
        >
        <a
          class="menu-item"
          target="_blank"
          href="https://freelancehunt.com/freelancer/Iriska_Ik.html"
          >Freelancehunt</a
        >
        <a class="menu-item" target="_blank" href="https://t.me/Iriska_IK"
          >Telegram</a
        >
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      MainfirstColor: "#73a9ff",
      MainsecondColor: "#ecf3ff",
      MaintextColor: "#fff",
      firstColor: "#73a9ff",
      secondColor: "#ecf3ff",
      textColor: "#fff",
      isColorPicker: false,
      isBgSet: false,
      link: "",
    };
  },
  methods: {
    useBg() {
      document.body.style.backgroundImage = `url(${this.link})`
      this.isBgSet = false;
    },
    cancelBg() {
      this.link = "";
      this.isBgSet = false;
    },
    setMainColor() {
      this.firstColor = this.MainfirstColor;
      this.textColor = this.MaintextColor;
      this.$emit("setStartColor");
    },
    setBg() {
      this.isBgSet = true;
    },
  },
  watch: {
    firstColor: function (newColor, oldColor) {
      this.$emit("changeColorAdd", newColor);
    },
    secondColor: function (newColor, oldColor) {
      this.$emit("changeSecondColor", newColor);
    },
    textColor: function (newColor, oldColor) {
      this.$emit("changeText", newColor);
    },
  },
};
</script>

<style>
.dropbtn {
  background-color: inherit;
  color: white;
  font-size: 16px;
  border: none;
  font-family: "Oswald", sans-serif;
  text-align: center;
}
.dropdown {
  position: relative;
  display: block;
  transition: all 0.2s;
}
.dropdown:hover {
  background-color: rgb(102, 148, 223);
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  max-width: 250px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content .menu-item {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content .menu-item:hover {
  background-color: #ddd;
}

.dropdown:hover .dropdown-content {
  display: block;
}

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
.color-picker {
  display: none;
}

.color-item:hover .color-picker {
  display: list-item;
}
.cl_item {
  margin-right: 5px;
}
.set-bg {
  display: flex;
}
.link_inner {
  display: flex;
  height: 23px;
}
.link_input {
  height: 20px;
  width: 130px;
}
.link-holder {
  width: 68px;
  margin-right: 5px;
}
</style>