<template>
  <div class="app">
    <div class="header">Wishlist: {{ wishlistCount }}</div>

    <main class="container">
      <section class="controls">
        <h1>Available Courses</h1>
        <p class="sub">Save those you like to your wishlist.</p>
      </section>

      <section class="grid">
        <CourseCard
          v-for="course in courses"
          :key="course.id"
          :course="course"
          @save="onSave"
        />
      </section>
    </main>

    <footer class="footer">
      © 2025 BEST KITCHEN
    </footer>
  </div>
</template>

<script>
import { ref } from "vue";
import CourseCard from "./components/coursecard.vue";
import coursesData from "./data/courses.js";

export default {
  name: "App",
  components: { CourseCard },

  setup() {
    const courses = ref(coursesData);
    const wishlistCount = ref(0);
    const savedIds = new Set();

    const onSave = (id) => {
      if (!savedIds.has(id)) {
        savedIds.add(id);
        wishlistCount.value++;
      }
    };

    return { courses, wishlistCount, onSave };
  },
};
</script>

<style>
:root {
  --pink-light: #ffe3f3;
  --pink: #ff9acb;
  --pink-dark: #ff69b4;
  --bg: #fff7fb;
  --text: #fface2;
  --card-bg: #ffffff;
  --shadow: #fface2;
}

body {
  font-family: "Poppins", Inter, ui-sans-serif, system-ui, Helvetica, Arial;
  margin: 0;
  background: var(--bg);
  color: var(--text);
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: var(--bg);
  padding-bottom: 40px;
}

.header {
  background: var(--pink);
  padding: 1rem;
  text-align: center;
  color: white;
  font-size: 1.2rem;
  font-weight: bold;
  border-bottom: 3px solid var(--pink-dark);
}

.container {
  width: 100%;
  max-width: 1100px;
  margin: 1.2rem auto;
  padding: 0 1rem;
}

.controls h1 {
  margin: 0;
  font-size: 2rem;
  color: var(--pink-dark);
}

.sub {
  color: #fface2;
  margin-bottom: 1rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 25px;
}

.footer {
  text-align: center;
  color: #fface2;
  margin-top: 20px;
  padding: 1rem 0;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  gap: 200px;
}

:root {
  --brand: #fface2;
  --accent: #fdfdfd;
  --muted: #ffb0dc;
  --bg: #f6f8fa;
}

body {
  font-family: Inter, ui-sans-serif, system-ui, Helvetica, Arial;
  margin: 0;
  background: var(--bg);
  color: var(--brand);
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.container {
  width: 100%;
  max-width: 1100px;
  margin: 1.2rem auto;
  padding: 0 1rem;
}

.controls h1 {
  margin: 0 0 0.25rem 0;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 20px;
}
</style>
