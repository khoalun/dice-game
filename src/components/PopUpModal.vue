<script setup lang="ts">
// Logic here
</script>

<template>
  <div class="wrapper-popup">
    <div class="container">
      <div class="cookies-content" id="cookiesPopup">
        <button class="close">✖</button>
        <img src="https://cdn-icons-png.flaticon.com/512/1047/1047711.png" alt="cookies-img" />
        <p>We use cookies for improving user experience, analytics and marketing.</p>
        <button class="accept">That's fine!</button>
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
}
</style>
