<template>
  <div>
    <div class="header">
      <img src="@/assets/friends-icon.svg" alt="" />
      <p>Friends List</p>
    </div>
    <div class="bottom-area">
      <router-link to="/">
        <img class="icon" src="@/assets/home-icon.svg" alt="" />
      </router-link>
      <router-link to="/about">
        <img class="icon" src="@/assets/abt-icon.svg" alt="" />
      </router-link>
    </div>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: "Poppins", sans-serif;
  background-color: #e5e5e5;
  min-height: 100vh;
  height: 100%;
  max-width: 100%;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.header {
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: center;
  background-color: #5c3fd7;
  color: #fff;
  padding: 10px;
}

.header p {
  padding: 10px;
}

img {
  max-width: 100%;
}

.icon {
  transition: 0.5s;
}

.router-link-exact-active .icon {
  transform: scale(1.2) translateY(-7px);
}

.bottom-area {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #fff;
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 76px;
  box-shadow: 0px 0 3px rgba(143, 143, 143, 0.8);
  z-index: 2;
}
</style>
