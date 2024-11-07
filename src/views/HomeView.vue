<template>
  <div class="container">
    <div class="buttonGroup">
      <button @click="addElement" class="niceButton" style="margin-right: 20px">
        +
      </button>
      <button class="niceButton" @click="removeElement">-</button>
    </div>
    <div class="box">
      <div
        v-for="(item, index) in elements"
        :key="index"
        class="element"
        @click="navigateToPage(item)"
      >
        点击跳转
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
export default {
  setup() {
    const elements = ref(['about']);
    const router = useRouter();
    let cur = 0;
    const addElement = () => {
      elements.value.push(cur ? 'about' : 'about2');
      cur = !cur;
      console.log('dasd');
    };

    const removeElement = () => {
      if (elements.value.length > 0) elements.value.pop();
    };

    const navigateToPage = (name) => {
      router.push(`/${name}`);
    };
    return {
      removeElement,
      navigateToPage,
      addElement,
      elements,
    };
  },
};
</script>
<style lang="scss">
.container {
  width: 50%;
  border: 1px solid deepskyblue;
  margin: auto;
  height: 100vh;
  overflow-y: scroll;
  .buttonGroup {
    margin: 20px 0;
  }
  .box {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    .element {
      margin: 20px;
      width: 200px;
      height: 100px;
      background-color: #b9cacf;
      border-radius: 30px;
      line-height: 100px;
      border: 4px solid darkblue;
      font-size: medium;
    }
  }
}
.niceButton {
  position: relative;
  background-color: rgb(32, 93, 224);
  border: none;
  font-size: 28px;
  color: #ffffff;
  padding: 20px;
  width: 200px;
  text-align: center;
  transition-duration: 0.6s;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
}
.niceButton2::after {
  content: '';
  background: #53a4f0;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s;
}
.niceButton2:active::after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s;
}
</style>
