<script setup>
  import { ref } from 'vue'

  const fontColor = ref("")
  const computedFontSize = ref(2.5)
  const titleSize = () => `${computedFontSize.value}rem`

  const getFontColor = () => {
    return CSS.supports('color', fontColor.value.toLowerCase()) ? fontColor.value : "#fff"
  }

  const isValidColor = () => {
    
    if (fontColor.value.length) {
      return CSS.supports('color', fontColor.value.toLowerCase())
    }
    return true
  }

  const enlargeText = () => computedFontSize.value += .1

  const reduceText = () => computedFontSize.value -= .1
</script>

<template>
  <header id="header">
    <h1 class="header-title"
    :style="{fontSize: titleSize}">
      This is the header title
    </h1>
    <h3 class="header-subtitle">
      This is the header subtitle
    </h3>
    <p class="content">
      This is the header content
    </p>
  </header>
  <main id="main">
    <p class="content">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aliquam velit qui quaerat, ex architecto, labore maiores sint nam nulla perspiciatis dignissimos eos reprehenderit. Voluptatem at placeat voluptatum veritatis eum sapiente commodi praesentium alias, eaque eligendi deserunt quaerat ad delectus impedit?
    </p>
    <input class="text-input" type="text" v-model="fontColor" placeholder="Type a font color...">
    <br/>
    <p class="is-valid" v-if="!isValidColor()">
      <span class="tilt">Warning: </span>
      The input is not a valid CSS font color...
    </p>
    <div class="wrapper">
      <button class="btn-rounded"
      @click="enlargeText">
      +
      </button>
      <button class="btn-rounded"
      @click="reduceText">
        -
      </button>
    </div>
    <p class="label">
      Change title's font size...
    </p>
  </main>
</template>

<style scoped lang="scss">
  * {
    width: 90vh;
    margin: 0 auto;
  }
  #header {
    color: #fff;

    .header-title {
      text-align: center;
      margin: 15px auto;
      font-size: v-bind(titleSize());
    }
    .header-subtitle {
      font-weight: 500;
      text-align: center;
      margin-bottom: 50px;
    }
    .content {
      color: #fff;
      margin: 20px auto;
    }
  }

  .content {
    font-weight: 400;
    font-size: 1.2rem;
    color: v-bind(getFontColor());
    margin: 15px auto;
  }

  .btn-rounded {
    background: none;
    border: 2px solid white;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    color: #fff;
    font-size: 1.2rem;
  }

  .wrapper {
    display: flex;
    gap: 20px;
    width: 150px;
    margin: 30px auto;
    justify-content: space-around;
  }
  .label {
    margin: 0 auto;
    text-align: center;
    color: #fff;
  }

  span {
    margin-top: 10px;
  }

  .is-valid {
    color: orange;

    .tilt {
      color: firebrick;
      animation: tilt 600ms infinite;
    }
  }

  .text-input {
    width: 15rem;
    height: 1.5rem;
    font-size: 1.2rem;
    color: #777;
  }

  @keyframes tilt {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1
    }
  }
</style>
