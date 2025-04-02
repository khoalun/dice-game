<script setup lang="ts">
import { defineProps, computed } from 'vue'

const props = defineProps({
  isOpenPopup: { type: Boolean, default: false },
})

const getClassPopup = computed(() => {
  return {
    'open-popup': props.isOpenPopup,
  }
})

const emit = defineEmits<{
  (e: 'handleConfirm'): void
  (e: 'closeModal'): void
}>()

const confirm = () => {
  emit('handleConfirm')
  console.log('confirm popupVue')
}

const handleClose = () => {
  emit('closeModal')
}
</script>

<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
    <div class="container">
      <div class="cookies-content" id="cookiesPopup">
        <button class="close" v-on:click="handleClose">✖</button>
        <img src="https://cdn-icons-png.flaticon.com/512/1047/1047711.png" alt="cookies-img" />
        <p>We use cookies for improving user experience, analytics and marketing.</p>
        <button class="accept" v-on:click="confirm">That's fine!</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper-popup {
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
  background-color: #f5f5f5;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
}

.open-popup {
  opacity: 1 !important;
  visibility: visible !important;
}

.cookies-content {
  width: 320px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  color: #000;
  text-align: center;
  border-radius: 20px;
  padding: 30px 30px 70px;
}

.cookies-content .close {
  width: 30px;
  font-size: 20px;
  color: #c0c5cb;
  align-self: flex-end;
  background-color: transparent;
  border: none;
  margin-bottom: 10px;
  cursor: pointer;
}

.cookies-content img {
  width: 82px;
  margin-bottom: 15px;
}

.cookies-content p {
  margin-bottom: 40px;
  font-size: 18px;
}

.cookies-content .accept {
  background-color: #ed6755;
  border: none;
  border-radius: 5px;
  width: 200px;
  padding: 14px;
  font-size: 16px;
  color: white;
  box-shadow: 0px 6px 18px -5px rgba(237, 103, 85, 1);
  cursor: pointer;
}
</style>
