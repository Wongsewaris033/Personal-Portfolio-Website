<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({ isDark: Boolean })

const visible = ref(false)
const sectionRef = ref(null)
let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.15 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())

const technicalSkills = [
  {
    name: 'User Research',
    level: 85,
    desc: 'Interviews, Surveys, Usability Testing'
  },
  {
    name: 'UI/UX Design (Figma)',
    level: 90,
    desc: 'Wireframing, Prototyping, Visual Design'
  },
  {
    name: 'Design Systems',
    level: 80,
    desc: 'Component Libraries, UI Consistency'
  },
  {
    name: 'Information Architecture',
    level: 75,
    desc: 'User Flows, Sitemap, Content Structure'
  },
  {
    name: 'Accessibility',
    level: 70,
    desc: 'Inclusive & Responsive Design'
  },
  {
    name: 'Tailwind CSS',
    level: 85,
    desc: 'Responsive Design, Utility-first Styling'
  },
  {
    name: 'HTML / CSS / JavaScript',
    level: 80,
    desc: 'Semantic HTML, Flexbox, Grid, ES6+'
  },
  {
    name: 'Vue.js',
    level: 75,
    desc: 'Components, Routing, Composition API'
  },
]

const softSkills = [
  'Communication',
  'Empathy',
  'Critical Thinking',
  'Problem Solving',
  'Collaboration & Teamwork',
  'Creativity',
  'Adaptability',
  'Time Management',
  'Attention to Detail',
  'User-Centered Thinking',
  'Analytical Thinking',
  'Research Mindset',
]

const process = [
  {
    step: '01',
    title: 'Research',
    desc: 'Understand user needs and business goals through interviews, observation, and competitive analysis.'
  },
  {
    step: '02',
    title: 'Define',
    desc: 'Synthesise findings into insights, personas, user journeys, and clear problem statements.'
  },
  {
    step: '03',
    title: 'Ideate',
    desc: 'Generate ideas and explore possible solutions through brainstorming and user flows.'
  },
  {
    step: '04',
    title: 'Prototype',
    desc: 'Create wireframes, interactive prototypes, and scalable design systems to visualise the product experience.'
  },
  {
    step: '05',
    title: 'Test & Iterate',
    desc: 'Conduct usability testing, gather feedback, and continuously refine the experience.'
  },
]
</script>

<template>
  <section id="skills" ref="sectionRef" class="py-28 md:py-36">
    <div class="max-w-7xl mx-auto px-10">

      <!-- Section header -->
      <div :class="['flex items-center gap-4 mb-20 transition-all duration-700', visible ? 'opacity-100' : 'opacity-0']">
        <span class="w-10 h-px bg-rose-400"></span>
        <span :class="['text-xs tracking-widest uppercase font-medium', isDark ? 'text-rose-400' : 'text-rose-500']">Skills &amp; Process</span>
      </div>

      <div class="grid lg:grid-cols-12 gap-16 xl:gap-24">

        <!-- Technical Skills bars -->
        <div class="lg:col-span-6">
          <h3 :class="['text-2xl font-semibold mb-10', isDark ? 'text-zinc-100' : 'text-zinc-900']">Technical Skills</h3>
          <div class="flex flex-col gap-6 mb-12">
            <div
              v-for="(skill, i) in technicalSkills"
              :key="i"
              :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4']"
              :style="{ transitionDelay: `${i * 80}ms` }"
            >
              <div class="flex justify-between items-baseline mb-2">
                <span :class="['text-sm font-semibold', isDark ? 'text-zinc-200' : 'text-zinc-800']">{{ skill.name }}</span>
                <span :class="['text-xs font-mono', isDark ? 'text-zinc-500' : 'text-zinc-500']">{{ skill.level }}%</span>
              </div>
              <div :class="['h-1.5 rounded-full overflow-hidden', isDark ? 'bg-zinc-800' : 'bg-zinc-200']">
                <div
                  class="h-full bg-rose-400 rounded-full transition-all duration-1000 ease-out"
                  :style="{ width: visible ? `${skill.level}%` : '0%', transitionDelay: `${200 + i * 80}ms` }"
                ></div>
              </div>
              <div :class="['text-[11px] mt-1.5', isDark ? 'text-zinc-600' : 'text-zinc-500']">{{ skill.desc }}</div>
            </div>
          </div>

          <!-- Soft Skills -->
          <h3 :class="['text-xl font-semibold mb-5', isDark ? 'text-zinc-100' : 'text-zinc-900']">Soft Skills</h3>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="(skill, i) in softSkills"
              :key="i"
              :class="[
                'px-4 py-2 text-xs rounded-sm border font-medium transition-all duration-700',
                isDark ? 'border-zinc-700 text-zinc-300 bg-zinc-900/40' : 'border-zinc-200 text-zinc-700 bg-white',
                visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
              ]"
              :style="{ transitionDelay: `${500 + i * 60}ms` }"
            >{{ skill }}</span>
          </div>
        </div>

        <!-- Process column -->
        <div class="lg:col-span-6">
          <h3 :class="['text-2xl font-semibold mb-10', isDark ? 'text-zinc-100' : 'text-zinc-900']">My Design Process</h3>
          <div class="flex flex-col gap-0">
            <div
              v-for="(step, i) in process"
              :key="i"
              :class="[
                'flex gap-6 transition-all duration-700',
                visible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-6'
              ]"
              :style="{ transitionDelay: `${i * 100}ms` }"
            >
              <div class="flex flex-col items-center">
                <div class="w-9 h-9 rounded-full border-2 border-rose-400 flex items-center justify-center shrink-0">
                  <span class="text-[9px] font-mono text-rose-400">{{ step.step }}</span>
                </div>
                <div
                  v-if="i < process.length - 1"
                  :class="['w-px flex-1 mt-1 mb-1', isDark ? 'bg-zinc-800' : 'bg-zinc-300']"
                  style="min-height: 2rem;"
                ></div>
              </div>
              <div class="pb-8">
                <div :class="['text-base font-semibold mb-1', isDark ? 'text-zinc-100' : 'text-zinc-900']">{{ step.title }}</div>
                <div :class="['text-sm leading-relaxed', isDark ? 'text-zinc-500' : 'text-zinc-600']">{{ step.desc }}</div>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>