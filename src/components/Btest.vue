<template>
  <div class="container">
    <div class="notifications">
      <div
        v-for="(toast, index) in toasts"
        :key="index"
        :class="['toster', toast.type, { hide: toast.isHiding }]"
      >
        <div class="icon">
          <i :class="toast.icon"></i>
        </div>
        <div class="tosterHeading">
          <h1>{{ toast.title }}</h1>
          <p>{{ toast.text }}</p>
        </div>
        <i class="fa-solid fa-xmark" @click="removeToast(index)"></i>
      </div>
    </div>
    <div class="buttonDiv">
      <button class="btn" @click="handleClick('success')">success</button>
      <button class="btn" @click="handleClick('error')">error</button>
      <button class="btn" @click="handleClick('warning')">warning</button>
      <button class="btn" @click="handleClick('info')">info</button>
    </div>
    <div class="copy-right">
      <p>
        Made With <a href="#">❤️</a> By
        <a href="https://jaimindev.blogspot.com">Jaimin Patel</a>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const toasts = ref([]);

function createTost(type, icon, title, text) {
  const newToast = {
    type,
    icon,
    title,
    text,
    isHiding: false,
  };
  toasts.value.push(newToast);
  // setTimeout(() => removeToast(toasts.value.indexOf(newToast)), 5000);
  setTimeout(() => hideToast(toasts.value.indexOf(newToast)), 5000);
}

const hideToast = (index) => {
  toasts.value[index].isHiding = true;
  toasts.value.forEach((toast, index) => {
    setTimeout(() => removeToast(index), index + 1 * 1000);
  });
};

function removeToast(index) {
  toasts.value.splice(index, 1);
}

function handleClick(type) {
  let icon = "";
  let title = "";
  let text = "";
  switch (type) {
    case "success":
      icon = "fa-solid fa-circle-check";
      title = "Success";
      text = "This is a Success toast.";
      break;
    case "error":
      icon = "fa-solid fa-circle-exclamation";
      title = "Error";
      text = "This is an Error toast.";
      break;
    case "warning":
      icon = "fa-solid fa-triangle-exclamation";
      title = "Warning";
      text = "This is a Warning toast.";
      break;
    case "info":
      icon = "fa-solid fa-circle-info";
      title = "Info";
      text = "This is an Info toast.";
      break;
    default:
      break;
  }
  createTost(type, icon, title, text);
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap");

body {
  font-family: "Poppins", sans-serif;
  background-color: #1c1d22;
}

:root {
  --successColor: #0abf3055;
  --errorColor: #f24d4c;
  --warningColor: #e9bd0c;
  --infoColor: #3498db;
}

.container {
  width: 100%;
  height: 100vh;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.btn {
  background-color: aqua;
  font-size: 1.5rem;
  font-weight: 600;
  padding: 1rem 2rem;
  margin: 1rem;
  text-align: center;
  border-radius: 5px;
  cursor: pointer;
}

.notifications {
  position: fixed;
  top: 2rem;
  right: 3rem;
}

.toster {
  position: relative;
  color: aliceblue;
  padding: 1rem 2rem;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: effect 0.3s ease 1 forwards;
  margin-bottom: 1rem;
}

@keyframes fadeOut {
  0% {
    transform: translateX(-10%);
  }

  100% {
    transform: translateX(calc(100% + 3rem));
  }
}

.toster.hide {
  animation: fadeOut 0.5s ease 1 forwards;
}

.success {
  --borderColor: #0abf3055;
  background-image: linear-gradient(to right, #0abf3055, #22242f 30%);
}

.error {
  --borderColor: #f24d4c;
  background-image: linear-gradient(to right, #f24d4c55, #22242f 30%);
}

.warning {
  --borderColor: #e9bd0c;
  background-image: linear-gradient(to right, #e9bd0c55, #22242f 30%);
}

.info {
  --borderColor: #3498db;
  background-image: linear-gradient(to right, #3498db55, #22242f 30%);
}

@keyframes effect {
  0% {
    transform: translateX(100%);
  }

  100% {
    transform: translateX(-10%);
  }
}

.toster::before {
  content: "";
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 6px;
  background-color: var(--borderColor);
  animation: tiumeOut 5s linear 1 forwards;
  box-shadow: 0 0 10px var(--borderColor);
}

@keyframes tiumeOut {
  to {
    width: 0;
  }
}

.icon {
  font-size: 1.5rem;
  margin-right: 1rem;
}

.tosterHeading {
  margin-right: 1.3rem;
}

.copy-right {
  position: absolute;
  bottom: 1rem;
  color: white;
  font-weight: 600;
}

.copy-right a {
  color: white;
  text-decoration: none;
}

.copy-right-success {
  color: var(--successColor);
  text-shadow: 2px 2px 8px var(--successColor);
}

.copy-right-error {
  color: var(--errorColor);
  text-shadow: 2px 2px 8px var(--errorColor);
}

.copy-right-warning {
  color: var(--warningColor);
  text-shadow: 2px 2px 8px var(--warningColor);
}

.copy-right-info {
  color: var(--infoColor);
  text-shadow: 2px 2px 8px var(--infoColor);
}
</style>
