<template>
  <nav class="navbar">
    <div class="column-1">
      <router-link :to="{ name: 'Home' }" class="homelink"
        >Luminescence</router-link
      >
    </div>

    <div class="column-2">
      <router-link :to="{ name: 'About' }" class="link">About</router-link>
      <router-link :to="{ name: 'Categories' }" class="link">Categories</router-link>
      <router-link :to="{ name: 'Schedule' }" class="link">Schedule</router-link>
      <router-link :to="{ name: 'Contact' }" class="link">Contact</router-link>
    </div>


    <div class="column-3">

      <button class="login-button" @click="showLogin">Login</button>

      <div class="login-overlay" v-if="showingLogin">
        <div class="login-container">
          <h2>Login</h2>
          <form>
            <div class="form-group">
              <input v-model="email" type="email" placeholder="Email" />
            </div>
            <div class="form-group">
              <input
                v-model="password"
                type="password"
                placeholder="Password"
              />
            </div>
            <button type="button" @click="login" :disabled="loggingIn">
              {{ loggingIn ? "Logging in..." : "Log in" }}
            </button>
          </form>
          <button class="close-button" @click="hideLogin">Cancel</button>
        </div>
      </div>

      <div class="outer-links">
          <a
          href="https://www.youtube.com/@ckmsc39th_luminescence"
          target="_blank"
          rel="noopener noreferrer"
          class="icon"
        >
          <vue-feather type="youtube" size="20"></vue-feather>
        </a>
        <a
          href="https://instagram.com/luminescence_ckmsc39th_"
          target="_blank"
          rel="noopener noreferrer"
          class="icon"
        >
          <vue-feather type="instagram" size="20"></vue-feather>
        </a>
      </div>
      
      <div class="mobile">
        <label class="hamburger-menu">
          <input @click="toggleNavbar" type="checkbox" id="checkID"/>
        </label>
          
        <aside class="sidebar-overlay">
          <div class="sidebar">
            <div class="mobile-link">
              <router-link :to="{ name: 'About' }" @click="uncheck" class="hover-mobile-link"
              >About</router-link>
            </div>

            <div class="seperated_line"></div>

            <div class="mobile-link">
              <router-link :to="{ name: 'Categories' }" @click="uncheck" class="hover-mobile-link"
              >Categories</router-link>
            </div>

            <div class="seperated_line"></div>

            <div class="mobile-link">
              <router-link :to="{ name: 'Schedule' }" @click="uncheck" class="hover-mobile-link"
              >Schedule</router-link>
            </div>

            <div class="seperated_line"></div>

            <div class="mobile-link">
              <router-link :to="{ name: 'Contact' }" @click="uncheck" class="hover-mobile-link"
              >Contact</router-link>
            </div>

            <div class="seperated_line"></div>
            <br>
            <div class="flex justify-evenly">
              <a
                href="https://www.youtube.com/@ckmsc39th_luminescence"
                target="_blank"
                rel="noopener noreferrer"
                class="mobile-icon"
              >
              <vue-feather type="youtube" size="20"></vue-feather>
              </a>
              <a
                href="https://instagram.com/luminescence_ckmsc39th_"
                target="_blank"
                rel="noopener noreferrer"
                class="mobile-icon"
              >
              <vue-feather type="instagram" size="20"></vue-feather>
              </a>
            </div>
            
          </div>
        </aside>
      </div>
    </div>

  </nav>
</template>

<script setup>
import { ref } from "vue";
import feather from "feather-icons";
feather.replace();

const email = ref("");
const password = ref("");
const loggingIn = ref(false);
const showingLogin = ref(false);
const showingNavbar = ref(false);

const correctEmail = "123@email.com";
const correctPasswd = "1234";

async function login() {
  loggingIn.value = true;
  try {
    if (email.value === correctEmail && password.value === correctPasswd) {
      console.log("true111");
    } else {
      console.log("false111");
    }
  } catch (error) {
    console.error(error);
  }
  loggingIn.value = false;
}

function toggleNavbar() {
  const body = document.body;
  showingNavbar.value = !showingNavbar.value

  if (showingNavbar.value){
    body.style.overflowY = 'hidden';
  }else{
    body.style.overflowY = '';
  }
}

function showLogin() {
  showingLogin.value = true;
}

function hideLogin() {
  showingLogin.value = false;
}

function uncheck() {
  let input = document.getElementById('checkID')
  input.checked = false;
  toggleNavbar()
}

</script>

<style>
:root{
  --bar-width: 30px;
  --bar-height: 4px;
  --gap: 6px;
  --hamburger-height: calc(var(--bar-height)*3 + var(--gap)*2);
  --x-width: calc(var(--hamburger-height) * 1.414213562)
}

nav.navbar {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5% 5%;
  background-color: rgba(55, 55, 55, 0.7);
}

.column-1{
  display: flex;
  align-items: center;
  gap: 1px
}

.column-2{
  display: flex;
  align-items: center;
  gap: 3px;

}

.column-3{
  display: flex;
  align-items: center;
}

.mobile{
  margin-right: 30px;
  display: flex;
  align-items: center;
}

.hamburger-menu{
  display: flex;
  flex-direction: column;
  gap: var(--gap);
  width: max-content;
  position: absolute;
  right: 20px;
  z-index: 10;
  cursor: pointer;
}

.hamburger-menu::before,
.hamburger-menu::after,
.hamburger-menu input{
  content: "";
  width: var(--bar-width);
  height: var(--bar-height);
  background-color: white;
  border-radius: 4px;
  transform-origin: left center;
  transition: opacity 200ms ease-in-out, 
              width 200ms ease-in-out,
              rotate 200ms ease-in-out,
              translation 200ms ease-in-out,
              background-color 200ms ease-in-out;
  z-index: 9999;
}

.hamburger-menu:has(input:checked)::before {
  rotate: 45deg;
  width: var(--x-width);
  translate: 0 calc(var(--bar-height) / -2);
}

.hamburger-menu:has(input:checked)::after {
  rotate: -45deg;
  width: var(--x-width);
  translate: 0 calc(var(--bar-height) / 2);
}

.hamburger-menu input{
  appearance: none;
  padding: 0;
  margin: 0;
  outline: none;
  pointer-events: none;
}

.hamburger-menu input:checked {
  opacity: 0;
  width: 0;
}

.sidebar-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  transition: translate 200ms ease-in-out;
  translate: 300%;
  background-color: rgba(33, 29, 41, 0.9);
  color: white;
  max-width: 100vw;
  min-height: 100vh;
}

.sidebar {
  font-weight: bold;
  width: 25%;
  height: 100vh;
  position: absolute;
  right: 40px;
  top: 100px;
}

.seperated_line {
  border: solid 1px rgba(241, 241, 241, 0.8);
}

.hamburger-menu:has(input:checked) + .sidebar-overlay{
  translate: 0;
}

.homelink {
  text-align: center;
  font-weight: bold;
  font-family: cursiveFont;
  padding: 5%;
  border-radius: 0.45em;
}

.homelink:hover {
  border-color: hsl(272, 71%, 81%);
  background-color: hsl(272, 71%, 81%);
  box-shadow: 0px 0px 0.5em 0.5px hsl(272, 100%, 81%);
  animation: text-flicker 3s linear infinite;
  color: rgb(55, 55, 55);
}

.link {
  min-width: fit-content;
  font-family: 'Recursive', sans-serif;
  font-weight: bold;
  border-radius: 0.45em;
  text-align: center;
  padding: 15px 2%;
}

.link:hover {
  border-color: hsl(186, 100%, 78%);
  background-color: hsl(186 100% 78%);
  box-shadow: 0px 0px 0.75em 1px hsl(186 100% 78%);
  animation: text-flicker 6s linear infinite;
  color: rgb(55, 55, 55);
}

.icon {
  align-items: center;
  border-radius: 0.5em;
  color: white;
}

.icon:hover {
  border-color: hsl(65, 100%, 89%);
  background-color: hsl(66, 83%, 93%);
  box-shadow: 0px 0px 0.5em 0px hsl(66, 83%, 93%);
  animation: text-flicker 6s linear infinite;
  color: black;
}

.mobile-link{
  font-family: 'Recursive';
  margin-top: 5px;
  margin-bottom: 5px;
  padding: 10%;
}

.mobile-link:has(.hover-mobile-link:hover) {
  border-radius: 0.25em;
  border-color: hsl(186, 100%, 78%);
  background-color: hsl(186 100% 78%);
  box-shadow: 0px 0px 0.75em 1px hsl(186 100% 78%);
  animation: text-flicker 6s linear infinite;
  color: black;
}

.mobile-icon{
  margin: 2%;
  padding: 10%;
}

.mobile-icon:hover{
  border-radius: 0.5em;
  border-color: hsl(65, 100%, 89%);
  background-color: hsl(66, 83%, 93%);
  box-shadow: 0px 0px 0.5em 0px hsl(66, 83%, 93%);
  animation: text-flicker 6s linear infinite;
  color: black;
}

.login-button {
  background-color: transparent;
  color: white;
  cursor: pointer;
  font-family: 'Recursive', sans-serif;
  font-weight: bold;
  border-radius: 0.45em;
  text-align: center;
  padding-top: 15px;
  padding-bottom: 15px;
}

.login-button:hover {
  border-color: hsl(104, 100%, 86%);
  border-radius: 0.45em;
  background-color: hsl(104, 100%, 86%);
  box-shadow: 0px 0px 0.75em 1px hsl(104, 100%, 86%);
  animation: text-flicker 6s linear infinite;
  color: black;
}

.login-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: fade-in-animation ease-in 0.2s;
}

.login-container {
  background-color: #fff;
  width: 280px;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  text-align: center;
  transform: translateY(0%);
  transition: transform 0.5s ease-in-out;
}

.login-container.show {
  transform: translateY(0);
}

.login-container h2 {
  margin-bottom: 30px;
  font-size: 24px;
  font-weight: bold;
  color: #333;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.login-container form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.login-container form .form-group {
  margin-bottom: 20px;
  width: 100%;
}

.login-container form label {
  display: block;
  margin-bottom: 5px;
  font-size: 14px;
  color: #555;
}

.login-container form input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: rgba(0, 105, 217, 0.7);
  transition: background-color 0.5s ease-in-out;
}

.login-container form input:focus {
  outline: none;
  background-color: #0069d9;
}

.login-container form button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.5s ease-in-out;
}

.login-container form button:hover {
  background-color: #0069d9;
}

.login-container form button:active {
  transform: scale(0.95);
}

.close-button {
  background-color: transparent;
  border: none;
  color: #888;
  font-size: 16px;
  cursor: pointer;
  margin-top: 20px;
}

::placeholder {
  /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #ddd;
  opacity: 1; /* Firefox */
}

::-ms-input-placeholder {
  /* Microsoft Edge */
  color: #ddd;
}

@media (max-width: 2000px) {
  .homelink{
    font-size: 3.75rem;
  }

  .link{
    font-size: 1.1rem;
    width: 100px;
  }

  .login-button{
    font-size: 1.1rem;
    width: 100px;
  }

  .icon{
    padding-top: 18px;
    padding-bottom: 18px;
    padding-left: 10px;
    padding-right: 10px;
  }
}

@media (max-width: 1100px) {
  .homelink{
    font-size: 3rem;
  }

  .link{
    font-size: 0.9rem;
    width: 70px;
  }

  .login-button{
    font-size: 0.9rem;
    width: 70px;
  }

  .icon{
    padding-left: 5px;
    padding-right: 5px;
    padding-top: 15px;
    padding-bottom: 15px;
  }
}

@media (max-width: 800px) {
  .column-2{
    display: none;
  }

  .outer-links{
    display: none;
  }

  .login-button{
    margin-right: 10px;
  }

  .hover-mobile-link {
    font-size: 0.9rem;
  }
}

@media (max-width: 480px){
  .login-button{
    margin-right: 20px;
    padding-left: 5px;
    padding-right: 5px;
  }
  .homelink{
    font-size: 2rem;
  }
}

@media (max-width: 380px){
  .homelink{
    font-size: 1.6rem;
  }

  .login-button{
    margin-right: 30px;
    padding-left: 3px;
    padding-right: 3px;
    width: 100%;
  }

  .hover-mobile-link {
    font-size: 0.8rem;
  }
}

@media (min-width: 801px) {
  .mobile{
    display: none;
  }
}
</style>
