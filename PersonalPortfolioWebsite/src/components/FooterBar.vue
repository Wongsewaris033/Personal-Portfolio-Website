<script setup>
defineProps({ isDark: Boolean })

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <footer :class="['py-10 border-t', isDark ? 'border-zinc-800' : 'border-zinc-100']">
    <div class="max-w-7xl mx-auto px-10">
      <div class="flex flex-col md:flex-row items-center justify-between gap-6">

        <!-- Copyright -->
        <span :class="['font-mono text-xs', isDark ? 'text-zinc-600' : 'text-zinc-400']">
          Wongsewaris Tumsud<span class="text-rose-400">.</span> © 2026
        </span>

        <!-- Quick Links -->
        <div class="flex items-center gap-6">
          <button
            v-for="item in ['about', 'work', 'skills', 'experience', 'contact']"
            :key="item"
            @click="scrollTo(item)"
            :class="[
              'text-[10px] tracking-widest uppercase font-medium transition-colors',
              isDark ? 'text-zinc-600 hover:text-zinc-300' : 'text-zinc-400 hover:text-zinc-700'
            ]"
          >{{ item }}</button>
        </div>

        <!-- Social Icons -->
        <div class="flex items-center gap-4">
          <a
            v-for="s in [{ label: 'GH', href: 'https://github.com/Wongsewaris033' },
            { label: 'LI', href: 'https://www.linkedin.com/in/wongsewaris-tumsud-02523840b/' },
            { label: 'FB', href: 'https://www.facebook.com/wongsewaris.tumsud/' },
            { label: 'IG', href: 'https://www.instagram.com/win_wwr/'}]"
            :key="s.label"
            :href="s.href"
            target="_blank"
            rel="noopener noreferrer"
            :class="[
              'w-8 h-8 rounded-sm border flex items-center justify-center text-[10px] font-bold transition-all duration-200 hover:scale-105',
              isDark
                ? 'border-zinc-700 hover:border-rose-400 hover:text-rose-400'
                : 'border-zinc-500 hover:border-rose-400 hover:text-rose-500 bg-white'
            ]"
          >{{ s.label }}</a>
        </div>

      </div>
    </div>
  </footer>
</template>