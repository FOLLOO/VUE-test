<script setup>
import Button from '../components/ui/bttons/Button.vue'
import Link from '../components/ui/links/Link.vue'

</script>

<template>
  <main class="main">
    <h1 class="titley">
      Привет!
    </h1>
    <p class="comment">
      Лайк за файл <code>data.json</code>, особенно  "Бургеркинг Когтевранович" — тоже люблю Гари Харламов и узник бульдогович!
    </p>
    <p class="project-info">
      В данном проекте я старался избежать использования сторонних библиотек и реализовал функциональность вручную, чтобы максимально точно соответствовать макету. Кроме того, применил CSS reset в файле <code>main.css</code>.
    </p>
    <p class="features">
      Для фильтрации данных была реализовал функциональность поиска, а также пагинация.
    </p>

    <Link
        :isActive=true
        text="Результат тут"
        href="/study_session"
    />
  </main>
</template>

<style scoped>
.main{
  max-width: 500px;
  margin: auto;
}
.titley {
  font-size: 2em;
  margin-bottom: 20px;
  color: var(--accent);
  text-align: left;
}

.comment {
  font-style: italic;
  margin: 10px 0;
  color: #555;
}

.project-info {
  margin: 15px 0;
  padding: 10px;
  background-color: #fff;
  border-left: 4px solid var(--accent);
}

.features {
  margin: 15px 0;
  background-color: #e3f2fd;
  padding: 10px;
  border-radius: 5px;
}

code {
  background-color: #f1f1f1;
  padding: 2px 4px;
  border-radius: 3px;
}
</style>
