<script setup>
import {RouterLink, RouterView, useRoute} from 'vue-router'
import Link from "@/components/ui/links/Link.vue";
import calendar from "@/assets/icons/CalendarBlank.svg"
import accentGuard from "@/assets/icons/GraduationCap.svg"
import door from "@/assets/icons/Door.svg"
import student from "@/assets/icons/Student.svg"
import userList from "@/assets/icons/UserList.svg"
import zip from "@/assets/icons/zip.svg"
import settings from "@/assets/icons/settings.svg"
import video from "@/assets/icons/video.svg"
import logout from '@/assets/icons/log-out.svg'
import logo from "@/assets/logo.svg"
import Profile from "@/components/ui/porfiles/Profile.vue";
import {PROJECT_NAME} from "../utils.js";

const route = useRoute()

const menuItems = [
  {
    to: "/schedule",
    text: "Расписание",
    image: calendar,
  },
  {
    to: "/study_session",
    text: "Учебные сессии",
    image: accentGuard,
  },
  {
    to: "/rooms",
    text: "Список комнат",
    image: door,
  },
  {
    to: "/users",
    text: "Пользователи",
    image: student,
  },
  {
    to: "/student_rooms",
    text: "Учебные комнаты",
    image: userList,
  },
  {
    to: "/apps",
    text: "Список устройств",
    image: video,
  },
  {
    to: "/settings",
    text: "Настройка системы",
    image: settings,
  },
  {
    to: "/zip",
    text: "Архив",
    image: zip,
  },
];

</script>

<template>
  <label for="cheese" class="menu-label"> < </label>
  <input type="checkbox" class="menu" name="cheese" id="cheese" @input="console.log('yjhhfgh')" />
  <header class="App-header">
    <div class="wrapper">
      <div class="content">
        <a class="logo" href="/">
          <img :src="logo" :alt="PROJECT_NAME"/>
          <h1 class="logo-title">{{ PROJECT_NAME }}</h1>
        </a>
        
        <nav class="nav">
          <RouterLink
              v-for="(item, index) in menuItems"
              :key="index"
              :to="item.to"
          >
            <Link
                :isActive="route.path === item.to"
                type="default"
                :text="item.text"
                :image="item.image"
            />
          </RouterLink>
        </nav>
      </div>
      <div class="footer">

        <Profile
            status="Преподаватель"
            name="Нафис Сафиуллни"
        />

        <Link
            href="/"
            :isActive="false"
            type="outlet"
            text="Выйти"
            :image="logout"
        />

        <p class="des">Версия 1.02</p>
      </div>

    </div>
  </header>
  <RouterView/>
</template>

<style scoped>

/* .sidebar_input[name="check-in"]{
    position: absolute;
    visibility: hidden;
} */

.menu-label{
  background-color: black;
  border-radius: 100%;
  width: 1.5rem;
  padding: 0 .5rem;
  font-size: var(--text-sm);
  height: 1.5rem;
  position: relative;
  color: white;
  left: 15vw;
  top: 3vh;
}


.menu:not(:checked) + .App-header{
    max-width: 15vw;
    transition: all .5s ease;
}

.menu:checked ~ .menu-label{
  left: 5vw;
}
.menu:checked + .App-header {
    max-width: 1vw;
    transition: all .5s ease;
    visibility: hidden;
  }


.footer {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.content {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.logo {
  display: flex;
  gap: 1rem;
  width: 100%;
  align-items: center;
  justify-content: center;
}

.logo-title {
  font-size: var(--text-2xl);
  font-weight: bold;
}

.des {
  font-size: var(--text-sm);
  color: var(--t-c-description);
}

.App-header {
  background: var(--color-background);

  padding: 1rem;
  width: 100vh;
  height: 100vh;
  max-width: 300px;
}

.nav {
  display: flex;
  flex-direction: column;
  gap: .2rem;
}

.wrapper {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: space-between;
}
</style>
