<script setup>
import { ref, watch, onMounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import WorkSection from './components/WorkSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterBar from './components/FooterBar.vue'

const isDark = ref(true)

onMounted(() => {
  const saved = localStorage.getItem('theme')
  if (saved) isDark.value = saved === 'dark'
})

watch(isDark, (val) => {
  localStorage.setItem('theme', val ? 'dark' : 'light')
})

function toggleTheme() {
  isDark.value = !isDark.value
}
</script>

<template>
  <div
    :class="[
      'min-h-screen transition-colors duration-500',
      isDark ? 'bg-zinc-950 text-zinc-100' : 'bg-stone-50 text-zinc-900'
    ]"
  >
    <NavBar :isDark="isDark" @toggleTheme="toggleTheme" />
    <HeroSection :isDark="isDark" />
    <AboutSection :isDark="isDark" />
    <WorkSection :isDark="isDark" />
    <SkillsSection :isDark="isDark" />
    <ExperienceSection :isDark="isDark" />
    <ContactSection :isDark="isDark" />
    <FooterBar :isDark="isDark" />
  </div>
</template>