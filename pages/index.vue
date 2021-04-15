<template>
  <div class="container">
    <div class="outer-container">
      <h1>Just a Super Mario Jump</h1>
      <div class="coin-counter">
        <img src="@/assets/coin.png" />
        <span>{{ count }}</span>
      </div>
      <div class="inner-container">
        <div :class="['coin', { appear: isAppear }]">
          <img src="@/assets/coin.png" />
        </div>
        <div
          :class="['block', { bounce: isBounce }]"
          @animationend="removeAnimation"
        >
          <img src="@/assets/block.png" />
        </div>
        <div
          :class="['mario', { jump: isJump }]"
          @animationend="isJump = false"
        >
          <img src="@/assets/mario.png" alt="mario" />
        </div>
        <div class="control">
          <button @click.prevent="jump">Press here to jump or space</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      isAppear: false,
      isBounce: false,
      isJump: false,
    }
  },
  beforeMount() {
    window.addEventListener('keydown', this.key)
  },
  methods: {
    key(e) {
      const code = e.keyCode
      if (code === 32) {
        this.jump()
      }
    },
    jump() {
      this.isAppear = true
      this.isBounce = true
      this.isJump = true
    },
    removeAnimation() {
      this.isAppear = false
      this.isBounce = false
      this.count++
    },
  },
}
</script>

<style>
/* ==================
 *  BASE
 * ================== */

.outer-container {
  background: url('@/assets/background.png') repeat-x;
  background-position-y: bottom;
  height: 607px;
  animation: moving_bg 75s linear infinite;
}
@media only screen and (max-width: 600px) {
  .outer-container {
    height: 665px;
  }
}
.inner-container {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-top: -55px;
}
h1 {
  background: var(--black);
  color: white;
  font-size: 40px;
  letter-spacing: 1px;
  margin: 0;
  padding: 20px 0;
  text-align: center;
  width: 100%;
}
.coin-counter {
  align-items: center;
  background: rgb(0, 0, 0, 0.1);
  border-radius: 3px;
  display: flex;
  margin: 0 20px;
  padding: 10px 10px 10px 20px;
  width: 80px;
}
.coin-counter img {
  margin-right: 13px;
  width: 32px;
}
.coin-counter span {
  font-size: 30px;
}
/* ==================
*  COIN
* ================== */
.coin {
  width: 80px;
}
.coin {
  height: 100px;
  position: relative;
  width: 60px;
}
.coin img {
  bottom: var(--coin-bottom-gone);
  position: absolute;
  width: 100%;
}
.coin.appear img {
  animation-delay: 0.1s;
  animation: appear 1.8s cubic-bezier(0.87, -0.41, 0.19, 1.44);
}
/* ==================
*  BLOCK
* ================== */
.block {
  height: 100px;
  position: relative;
  width: 90px;
  z-index: 100;
}
.block img {
  bottom: 0;
  position: absolute;
  width: 100%;
}
.block.bounce img {
  animation-delay: 0.1s;
  animation: bounce 1s cubic-bezier(0.87, -0.41, 0.19, 1.44);
}
/* ==================
*  MARIO
* ================== */
.mario {
  display: flex;
  height: 200px;
  justify-content: center;
  position: relative;
  width: 100px;
}
.mario img {
  bottom: 0;
  display: block;
  position: absolute;
  width: 100%;
}
.mario.jump img {
  animation-duration: 1s;
  animation-name: jump;
  animation-timing-function: cubic-bezier(0.87, -0.41, 0.19, 1.44);
}
/* ==================
*  CONTROL
* ================== */
.control {
  width: 100%;
}
button {
  background-color: rgb(0, 0, 0, 1);
  background-color: var(--green);
  border-bottom: 3px dashed var(--black);
  border-top: 3px dashed var(--black);
  border: 1px dotted transparent;
  border: 1px solid var(--black);
  color: var(--white);
  cursor: pointer;
  font-size: 18px;
  font-weight: bold;
  justify-content: center;
  padding: 8px 5px;
  text-align: center;
  text-transform: uppercase;
  width: 100%;
}
button:hover {
  background-color: var(--green-hover);
}
button:focus {
  outline: 0;
}
/* ==================
*  ANIMATION
* ================== */
@keyframes jump {
  0% {
    bottom: 0;
  }
  50% {
    bottom: 91px;
  }
  100% {
    bottom: 0;
  }
}

@keyframes bounce {
  0% {
    bottom: 0;
    z-index: 100;
  }
  50% {
    bottom: 20px;
  }
  100% {
    bottom: 0;
  }
}

@keyframes appear {
  0% {
    bottom: var(--coin-bottom-gone);
    opacity: 0;
  }
  30% {
    opacity: 1;
  }
  50% {
    bottom: var(--coin-bottom-appear);
  }
  90% {
    bottom: var(--coin-bottom-appear);
    transform: perspective(600px) rotateY(360deg);
  }
  100% {
    opacity: 0;
  }
}

@keyframes moving_bg {
  0% {
    background-position: 0 bottom;
  }
  100% {
    background-position: -2122px;
  }
}
</style>
