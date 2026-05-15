<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({ isDark: Boolean })

const visible = ref(false)
const sectionRef = ref(null)
let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.1 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())

const experiences = [
  {
    type: 'Coursework',
    period: '2024 – Present',
    title: 'Bachelor of School of Information Technology',
    org: 'King Mongkuts University of Technology Thonburi (KMUTT)',
    desc: 'Relevant coursework: CSS Framework (Vue.js + Tailwind), Web Application Development, Database Systems, UI/UX Design Principles, Human-Computer Interaction.',
    badge: 'Academic',
    badgeColor: 'blue',
  },
  {
    type: 'Academic Activity',
    period: '25-27 April 2026',
    title: 'SIT Camp 2026',
    org: 'School of Information Technology',
    desc: 'Be a group mentor to support and guide camp participants in all aspects of web development, including UX/UI design and frontend development.',
    badge: 'Volunteer',
    badgeColor: 'emerald',
  },
  {
    type: 'Certification',
    period: 'September 2024',
    title: 'Coursera Certifications',
    org: 'Learning How to Learn: Powerful mental tools to help you master tough subjects',
    desc: 'Completed the course Learning How to Learn: Powerful mental tools to help you master tough subjects, gaining effective learning techniques, memory strategies, and problem solving skills for mastering challenging subjects.',
    badge: 'Certificate',
    badgeColor: 'amber',
  },
  {
    type: 'Certification',
    period: 'March 2026',
    title: 'Coursera Certifications',
    org: 'Learn Bootstrap',
    desc: 'Completed a comprehensive course on Bootstrap, learning responsive web design, layout systems, components, and modern frontend development practices.',
    badge: 'Certificate',
    badgeColor: 'amber',
  },
  {
    type: 'Certification',
    period: 'March 2026',
    title: 'Coursera Certifications',
    org: 'Fundamentals of VueJS',
    desc: 'Completed a course on the fundamentals of Vue.js, covering component-based development, reactivity, routing, state management, and building interactive web applications.',
    badge: 'Certificate',
    badgeColor: 'amber',
  },
  {
    type: 'Certification',
    period: 'March 2026',
    title: 'Coursera Certifications',
    org: 'Learn Tailwind CSS',
    desc: 'Completed a course on Tailwind CSS, learning utility-first styling, responsive design, custom layouts, and modern UI development practices.',
    badge: 'Certificate',
    badgeColor: 'amber',
  },
]

const badgePalette = {
  blue:    { dark: 'bg-blue-900/40 text-blue-400 border-blue-800',    light: 'bg-blue-50 text-blue-600 border-blue-200' },
  rose:    { dark: 'bg-rose-900/40 text-rose-400 border-rose-800',    light: 'bg-rose-50 text-rose-600 border-rose-200' },
  emerald: { dark: 'bg-emerald-900/40 text-emerald-400 border-emerald-800', light: 'bg-emerald-50 text-emerald-600 border-emerald-200' },
  amber:   { dark: 'bg-amber-900/40 text-amber-400 border-amber-800', light: 'bg-amber-50 text-amber-600 border-amber-200' },
}
</script>

<template>
  <section id="experience" ref="sectionRef" class="py-28 md:py-36">
    <div class="max-w-7xl mx-auto px-10">

      <!-- Section header -->
      <div :class="['flex items-center gap-4 mb-20 transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6']">
        <span class="w-10 h-px bg-rose-400"></span>
        <span :class="['text-xs tracking-widest uppercase font-medium', isDark ? 'text-rose-400' : 'text-rose-500']">Experience &amp; Activities</span>
      </div>

      <!-- Timeline -->
      <div class="relative">
        <!-- Vertical line -->
        <div
          :class="['absolute left-[18px] top-0 bottom-0 w-px hidden md:block', isDark ? 'bg-zinc-800' : 'bg-zinc-200']"
        ></div>

        <div class="flex flex-col gap-10">
          <div
            v-for="(exp, i) in experiences"
            :key="i"
            :class="[
              'md:pl-14 relative transition-all duration-700',
              visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'
            ]"
            :style="{ transitionDelay: `${i * 100}ms` }"
          >
            <!-- Dot on timeline -->
            <div
              :class="[
                'absolute left-0 top-3 w-9 h-9 rounded-full border-2 border-rose-400 items-center justify-center shrink-0 hidden md:flex',
                isDark ? 'bg-zinc-950' : 'bg-stone-50'
              ]"
            >
              <span class="w-2 h-2 rounded-full bg-rose-400"></span>
            </div>

            <!-- Card -->
            <div
              :class="[
                'p-6 rounded-sm border transition-all duration-300',
                isDark ? 'border-zinc-800 bg-zinc-900/30 hover:border-zinc-600' : 'border-zinc-200 bg-white hover:border-rose-200 shadow-sm'
              ]"
            >
              <div class="flex flex-wrap items-start justify-between gap-3 mb-3">
                <div>
                  <div :class="['text-[10px] tracking-widest uppercase mb-1', isDark ? 'text-zinc-500' : 'text-zinc-600']">{{ exp.type }} · {{ exp.period }}</div>
                  <h3 :class="['text-base font-semibold', isDark ? 'text-zinc-100' : 'text-zinc-900']">{{ exp.title }}</h3>
                  <div :class="['text-sm mt-0.5', isDark ? 'text-zinc-500' : 'text-zinc-600']">{{ exp.org }}</div>
                </div>
                <span
                  :class="[
                    'text-[10px] tracking-widest uppercase px-3 py-1.5 rounded-sm border font-semibold shrink-0',
                    isDark ? badgePalette[exp.badgeColor].dark : badgePalette[exp.badgeColor].light
                  ]"
                >{{ exp.badge }}</span>
              </div>
              <p :class="['text-sm leading-relaxed', isDark ? 'text-zinc-400' : 'text-zinc-700']">{{ exp.desc }}</p>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>