<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({ isDark: Boolean })

const visible = ref(false)
const sectionRef = ref(null)
let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.2 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())

const form = ref({ name: '', email: '', message: '' })
const errors = ref({ name: '', email: '', message: '' })
const touched = ref({ name: false, email: false, message: false })
const submitted = ref(false)

function validateEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

function validate() {
  errors.value.name    = !form.value.name.trim()    ? 'Full name is required.' : ''
  errors.value.email   = !form.value.email.trim()   ? 'Email is required.'
                       : !validateEmail(form.value.email) ? 'Enter a valid email.' : ''
  errors.value.message = !form.value.message.trim() ? 'Message is required.' : ''
}

function handleBlur(field) {
  touched.value[field] = true
  validate()
}

function handleSubmit() {
  touched.value = { name: true, email: true, message: true }
  validate()
  if (errors.value.name || errors.value.email || errors.value.message) return
  submitted.value = true
  form.value = { name: '', email: '', message: '' }
  touched.value = { name: false, email: false, message: false }
  errors.value  = { name: '', email: '', message: '' }
  setTimeout(() => (submitted.value = false), 5000)
}

const socialLinks = [
  { label: 'GitHub',    href: 'https://github.com/Wongsewaris033',                         icon: 'GH' },
  { label: 'LinkedIn',  href: 'https://www.linkedin.com/in/wongsewaris-tumsud-02523840b/', icon: 'LI' },
  { label: 'Facebook',  href: 'https://www.facebook.com/wongsewaris.tumsud/',              icon: 'FB' },
  { label: 'Instagram', href: 'https://www.instagram.com/win_wwr/',                        icon: 'IG' },
]
</script>

<template>
  <section id="contact" ref="sectionRef" class="py-24 md:py-32">
    <div class="max-w-5xl mx-auto px-6">

      <!-- Section header -->
      <div :class="['flex items-center gap-4 mb-16 transition-all duration-700', visible ? 'opacity-100' : 'opacity-0']">
        <span class="w-8 h-px bg-rose-400"></span>
        <span :class="['text-xs tracking-widest uppercase font-medium', isDark ? 'text-rose-400' : 'text-rose-500']">Contact</span>
      </div>

      <div class="grid md:grid-cols-2 gap-16 items-start">

        <!-- Left: Headline + contact info -->
        <div>
          <h2
            :class="[
              'text-3xl md:text-4xl font-light leading-snug mb-6 transition-all duration-700',
              isDark ? 'text-zinc-100' : 'text-zinc-900',
              visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'
            ]"
          >
            Let's work<br /><span class="font-semibold">together.</span>
          </h2>
          <p
            :class="[
              'text-sm leading-relaxed mb-8 transition-all duration-700 delay-100',
              isDark ? 'text-zinc-400' : 'text-zinc-600',
              visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'
            ]"
          >
            I'm actively seeking internship or co-op opportunities in UX/UI design and frontend development.
            Feel free to reach out — I'd love to connect!
          </p>

          <!-- Contact details -->
          <div class="flex flex-col gap-4 mb-8">
            <a
              href="mailto:winwin.co.th.well@gmail.com"
              :class="[
                'flex items-center gap-3 group transition-all duration-700',
                visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
              ]"
              style="transitionDelay: 150ms"
            >
              <span :class="['text-[10px] tracking-widest uppercase w-16 shrink-0', isDark ? 'text-zinc-600' : 'text-zinc-600']">Email</span>
              <span class="w-4 h-px bg-current opacity-30"></span>
              <span :class="['text-sm transition-colors duration-200', isDark ? 'text-zinc-300 group-hover:text-rose-400' : 'text-zinc-700 group-hover:text-rose-500']">
                winwin.co.th.well@gmail.com
              </span>
            </a>
            <a
              href="tel:0964047951"
              :class="[
                'flex items-center gap-3 group transition-all duration-700',
                visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'
              ]"
              style="transitionDelay: 220ms"
            >
              <span :class="['text-[10px] tracking-widest uppercase w-16 shrink-0', isDark ? 'text-zinc-600' : 'text-zinc-600']">Tel</span>
              <span class="w-4 h-px bg-current opacity-30"></span>
              <span :class="['text-sm transition-colors duration-200', isDark ? 'text-zinc-300 group-hover:text-rose-400' : 'text-zinc-700 group-hover:text-rose-500']">
                096-404-7951
              </span>
            </a>
          </div>

          <!-- Social Links -->
          <div
            :class="['transition-all duration-700 delay-300', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4']"
          >
            <div :class="['text-[10px] tracking-widest uppercase mb-3', isDark ? 'text-zinc-600' : 'text-zinc-400']">Find me on</div>
            <div class="flex items-center gap-3">
              <a
                v-for="s in socialLinks"
                :key="s.label"
                :href="s.href"
                target="_blank"
                rel="noopener noreferrer"
                :class="[
                  'px-4 py-2 text-xs font-semibold rounded-sm border transition-all duration-200 hover:scale-105',
                  isDark
                    ? 'border-zinc-700 text-zinc-300 hover:border-rose-400 hover:text-rose-400'
                    : 'border-zinc-300 text-zinc-600 hover:border-rose-400 hover:text-rose-500 bg-white'
                ]"
              >{{ s.label }}</a>
            </div>
          </div>
        </div>

        <!-- Right: Contact Form -->
        <div
          :class="[
            'p-8 rounded-sm border transition-all duration-700 delay-200',
            isDark ? 'border-zinc-800 bg-zinc-900/40' : 'border-zinc-200 bg-zinc-100',
            visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'
          ]"
        >
          <!-- Success message -->
          <div v-if="submitted" class="flex items-center gap-3 mb-6 p-4 rounded-sm bg-emerald-500/10 border border-emerald-500/30">
            <span class="w-2 h-2 rounded-full bg-emerald-400 shrink-0"></span>
            <span :class="['text-sm', isDark ? 'text-emerald-400' : 'text-emerald-600']">Message sent! I'll get back to you soon.</span>
          </div>

          <div class="flex flex-col gap-5">

            <!-- Name -->
            <div>
              <div class="flex items-center justify-between mb-2">
                <label :class="['text-[10px] tracking-widest uppercase', isDark ? 'text-zinc-500' : 'text-zinc-800']">
                  Your Name <span class="text-rose-400">*</span>
                </label>
                <transition name="err">
                  <span v-if="touched.name && errors.name" class="text-[10px] text-rose-400">
                    {{ errors.name }}
                  </span>
                </transition>
              </div>
              <input
                v-model="form.name"
                type="text"
                placeholder="Full Name"
                @blur="handleBlur('name')"
                :class="[
                  'w-full px-4 py-3 text-sm rounded-sm border outline-none transition-colors duration-200',
                  touched.name && errors.name
                    ? 'border-rose-400'
                    : isDark ? 'border-zinc-700 focus:border-rose-400' : 'border-zinc-300 focus:border-rose-400',
                  isDark
                    ? 'bg-zinc-800/60 text-zinc-100 placeholder-zinc-600'
                    : 'bg-white text-zinc-900 placeholder-zinc-400'
                ]"
              />
            </div>

            <!-- Email -->
            <div>
              <div class="flex items-center justify-between mb-2">
                <label :class="['text-[10px] tracking-widest uppercase', isDark ? 'text-zinc-500' : 'text-zinc-800']">
                  Email Address <span class="text-rose-400">*</span>
                </label>
                <transition name="err">
                  <span v-if="touched.email && errors.email" class="text-[10px] text-rose-400">
                    {{ errors.email }}
                  </span>
                </transition>
              </div>
              <input
                v-model="form.email"
                type="email"
                placeholder="name@example.com"
                @blur="handleBlur('email')"
                :class="[
                  'w-full px-4 py-3 text-sm rounded-sm border outline-none transition-colors duration-200',
                  touched.email && errors.email
                    ? 'border-rose-400'
                    : isDark ? 'border-zinc-700 focus:border-rose-400' : 'border-zinc-300 focus:border-rose-400',
                  isDark
                    ? 'bg-zinc-800/60 text-zinc-100 placeholder-zinc-600'
                    : 'bg-white text-zinc-900 placeholder-zinc-400'
                ]"
              />
            </div>

            <!-- Message -->
            <div>
              <div class="flex items-center justify-between mb-2">
                <label :class="['text-[10px] tracking-widest uppercase', isDark ? 'text-zinc-500' : 'text-zinc-800']">
                  Message <span class="text-rose-400">*</span>
                </label>
                <transition name="err">
                  <span v-if="touched.message && errors.message" class="text-[10px] text-rose-400">
                    {{ errors.message }}
                  </span>
                </transition>
              </div>
              <textarea
                v-model="form.message"
                rows="4"
                placeholder="Tell me about your project or opportunity..."
                @blur="handleBlur('message')"
                :class="[
                  'w-full px-4 py-3 text-sm rounded-sm border outline-none transition-colors duration-200 resize-none',
                  touched.message && errors.message
                    ? 'border-rose-400'
                    : isDark ? 'border-zinc-700 focus:border-rose-400' : 'border-zinc-300 focus:border-rose-400',
                  isDark
                    ? 'bg-zinc-800/60 text-zinc-100 placeholder-zinc-600'
                    : 'bg-white text-zinc-900 placeholder-zinc-400'
                ]"
              ></textarea>
            </div>

            <!-- Submit -->
            <button
              @click="handleSubmit"
              class="w-full py-3.5 text-xs tracking-widest uppercase font-semibold bg-rose-500 text-white rounded-sm hover:bg-rose-600 active:scale-95 transition-all duration-200"
            >
              Send Message →
            </button>

          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.err-enter-active, .err-leave-active { transition: opacity 0.2s, transform 0.2s; }
.err-enter-from, .err-leave-to       { opacity: 0; transform: translateX(4px); }
</style>