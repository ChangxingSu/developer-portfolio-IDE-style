<template>
  <div class="relative">
    <button
      @click="toggleDropdown"
      class="flex items-center space-x-2 px-3 py-2 rounded hover:bg-gray-700 dark:hover:bg-gray-600"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path v-if="isDark" fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd" />
        <path v-else fill-rule="evenodd" d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" clip-rule="evenodd" />
      </svg>
      <span class="text-sm">主题</span>
    </button>

    <div v-if="isOpen" class="absolute right-0 mt-2 w-48 rounded-md shadow-lg bg-white dark:bg-gray-800 ring-1 ring-black ring-opacity-5">
      <div class="py-1" role="menu">
        <button
          @click="setTheme('light')"
          class="w-full text-left px-4 py-2 text-sm hover:bg-gray-100 dark:hover:bg-gray-700"
          :class="{'bg-gray-100 dark:bg-gray-700': !isDark}"
        >
          Light Modern
        </button>
        <button
          @click="setTheme('dark')"
          class="w-full text-left px-4 py-2 text-sm hover:bg-gray-100 dark:hover:bg-gray-700"
          :class="{'bg-gray-100 dark:bg-gray-700': isDark}"
        >
          Dark Theme
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const isDark = ref(true)
const isOpen = ref(false)

onMounted(() => {
  // 从localStorage读取主题设置
  const theme = localStorage.getItem('theme') || 'dark'
  setTheme(theme)
})

const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const setTheme = (theme) => {
  isDark.value = theme === 'dark'
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', theme)
  isOpen.value = false
}

// 点击外部关闭下拉菜单
onClickOutside(isOpen, () => {
  isOpen.value = false
})
</script> 