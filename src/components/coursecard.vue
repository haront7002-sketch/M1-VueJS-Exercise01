<template>
  <article class="card">
    <div class="image-wrapper">
      <img :src="course.img" alt="Chef photo" class="chef-img" />
      <span v-if="!course.available" class="sold-out-badge">SOLD OUT</span>
    </div>

    <div class="card-header">
      <h3 class="title">{{ course.title }}</h3>
      <div class="tags">
        <span class="level">{{ course.skillLevel }}</span>
      </div>
    </div>

    <p class="chef">{{ course.chef }}</p>

    <div class="card-bottom">
      <span class="price">{{ course.price }}</span>
      <button class="save-btn" @click="saveCourse" :disabled="saved || !course.available">
        {{ saved ? "Saved" : "Save" }}
      </button>
    </div>
  </article>
</template>

<script>
import { ref } from "vue";

export default {
  name: "CourseCard",
  props: {
    course: { type: Object, required: true },
  },
  emits: ["save"],

  setup(props, { emit }) {
    const saved = ref(false);

    const saveCourse = () => {
      if (props.course.available && !saved.value) {
        saved.value = true;
        emit("save", props.course.id);
      }
    };

    return { saved, saveCourse };
  },
};
</script>

<style scoped>
.card {
  background: var(--card-bg);
  border-radius: 18px;
  padding: 18px;
  box-shadow: var(--shadow);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 22px rgba(255, 140, 200, 0.3);
}

.image-wrapper {
  width: 100%;
  height: 180px;
  overflow: hidden;
  border-radius: 14px;
  position: relative;
  margin-bottom: 12px;
}

.chef-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: scale 0.3s ease;
}

.card:hover .chef-img {
  scale: 1.05;
}

.sold-out-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: var(--pink-dark);
  color: white;
  padding: 6px 12px;
  font-weight: bold;
  border-radius: 10px;
  font-size: 0.75rem;
  box-shadow: 0 2px 6px rgba(255, 80, 160, 0.3);
}

.title {
  margin: 0;
  font-size: 1.2rem;
  color: var(--pink-dark);
}

.chef {
  margin: 8px 0;
  color: #725064;
  font-size: 0.9rem;
}

.tags {
  margin-top: 4px;
}

.level {
  display: inline-block;
  background: var(--pink-light);
  color: var(--pink-dark);
  padding: 4px 10px;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  border: 1px solid var(--pink);
}

.card-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 14px;
}

.price {
  font-weight: bold;
  color: var(--pink-dark);
  font-size: 1.1rem;
}

.save-btn {
  background: var(--pink);
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 20px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.2s ease;
}

.save-btn:hover:not(:disabled) {
  background: var(--pink-dark);
}

.save-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.image-wrapper {
  width: 250px;
  height: 200px;
  overflow: hidden;
  border-radius: 12px;
  position: relative;
}

.chef-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card {
  background: #fff;
  border-radius: 14px;
  padding: 15px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
}

.sold-out-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: #f673b7;
  color: white;
  padding: 6px 12px;
  font-weight: bold;
  border-radius: 6px;
}

.price {
  font-weight: bold;
  color: #f673b7;
}

.save-btn {
  background: #f673b7;
  color: white;
  border: none;
  padding: 8px 14px;
  border-radius: 8px;
  cursor: pointer;
}

.save-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
