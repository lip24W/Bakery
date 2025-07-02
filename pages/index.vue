<template>
  <div class="container main-content">
    <section class="has-text-centered mb-6">
      <h1 class="title is-1 mb-4">Булонька — уютная пекарня в Нижнем Новгороде</h1>
      <p class="is-size-4 mb-5" style="color: #d48fa6; font-weight: 500;">Почувствуй вкус настоящей домашней выпечки в самом центре города!</p>
      <img src="/bakery/croissant.jpg" alt="Пекарня Булонька" style="max-width: 420px; border-radius: 24px; box-shadow: 0 4px 32px #f3e1d6; margin: 0 auto;">
    </section>
    <section class="mb-6">
      <div class="columns is-multiline is-centered">
        <div class="column is-one-quarter has-text-centered" v-for="adv in advantages" :key="adv.text">
          <div style="display: flex; flex-direction: column; align-items: center;">
            <span style="font-size: 3rem; margin-bottom: 0.5rem;">{{ adv.icon }}</span>
            <div class="is-size-5" style="color: #d48fa6; font-weight: 600;">{{ adv.text }}</div>
          </div>
        </div>
      </div>
    </section>
    <section class="mb-6">
      <div class="slider-wrapper" style="display: flex; align-items: center; justify-content: center;">
        <button class="slider-arrow left" @click="prevSlide" aria-label="Предыдущая акция"></button>
        <div class="slider-box box" style="max-width: 600px; margin: 0 24px;">
          <h2 class="title is-4 mb-4 has-text-centered">Акции</h2>
          <div class="slider-content has-text-centered">
            <div class="slider-slide" style="display: inline-block; min-width: 260px;">
              <template v-if="currentSlide === 0">
                <img src="/bakery/birthday.jpg" alt="День рождения" style="max-width: 180px; border-radius: 16px; margin-bottom: 1rem; box-shadow: 0 2px 12px #f3e1d6;" />
              </template>
              <template v-if="currentSlide === 2">
                <img src="/bakery/student.jpg" alt="Студенческий билет" style="max-width: 180px; border-radius: 16px; margin-bottom: 1rem; box-shadow: 0 2px 12px #f3e1d6;" />
              </template>
              <h3 class="is-size-4 mb-2" style="color: #b48ead; font-weight: bold;">{{ promotions[currentSlide].title }}</h3>
              <div class="is-size-5 mb-2">{{ promotions[currentSlide].desc }}</div>
              <div class="is-size-6" style="color: #d48fa6;">{{ promotions[currentSlide].note }}</div>
            </div>
          </div>
          <div class="mt-3">
            <span v-for="(p, i) in promotions" :key="i" class="dot" :class="{ active: i === currentSlide }"></span>
          </div>
        </div>
        <button class="slider-arrow right" @click="nextSlide" aria-label="Следующая акция"></button>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const advantages = [
  { icon: '🥐', text: 'Свежая выпечка каждый день' },
  { icon: '🌱', text: 'Натуральные ингредиенты' },
  { icon: '☕', text: 'Ароматный кофе и чай' },
  { icon: '🏡', text: 'Уютная атмосфера' },
]

const promotions = [
  {
    title: 'Скидка 15% на День рождения!',
    desc: 'Покажите паспорт и получите скидку 15% на весь заказ в день рождения и 3 дня после.',
    note: 'Акция действует при предъявлении документа.'
  },
  {
    title: '10% на первый заказ',
    desc: 'Зарегистрируйтесь на сайте и получите скидку 10% на первый онлайн-заказ.',
    note: 'Скидка применяется автоматически.'
  },
  {
    title: 'Студентам — 12% скидка',
    desc: 'Покажите студенческий билет и получите скидку 12% на всё меню.',
    note: 'Только для очной формы обучения.'
  }
]
const currentSlide = ref(0)
let interval: any = null
function prevSlide() {
  currentSlide.value = (currentSlide.value + promotions.length - 1) % promotions.length
}
function nextSlide() {
  currentSlide.value = (currentSlide.value + 1) % promotions.length
}
onMounted(() => {
  interval = setInterval(() => {
    nextSlide()
  }, 3000)
})
onUnmounted(() => {
  clearInterval(interval)
})
</script>

<style scoped>
.slider-box {
  background: #fffdfa;
  border-radius: 24px;
  box-shadow: 0 4px 32px 0 #f3e1d6;
  border: none;
}
.dot {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f3e1d6;
  margin: 0 4px;
  transition: background 0.2s;
}
.dot.active {
  background: #b48ead;
}
.slider-wrapper {
  position: relative;
}
.slider-arrow {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  border: none;
  background: #f8c8dc;
  color: #fff;
  font-size: 2.2rem;
  box-shadow: 0 2px 8px #f3e1d6;
  cursor: pointer;
  transition: background 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
}
.slider-arrow.left::before, .slider-arrow.right::before {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}
.slider-arrow:hover {
  background: #e7bfae;
}
</style> 