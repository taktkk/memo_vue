<script setup>
  let isOpen = ref(false);  
  
  const beforeEnter = (el) => {
    el.style.height = '0';
  },
  const toggle = () => {
    isOpen.value = !isOpen.value;
  },
  const enter = (el) => {
    el.style.height = el.scrollHeight + 'px';
  },
  const beforeLeave = (el) => {
    el.style.height = el.scrollHeight + 'px';
  },
  const leave = (el) => {
    el.style.height = '0';
  }
      
</script>

<template>
  <div class="accordion">
          <a class="toggle" @click="toggle()">
            <slot name="title"></slot>
            <transition name="rotation">
              <i class="fas fa-chevron-down" v-if="!isOpen"></i>
            </transition>
            <transition name="rotation">
              <i class="fas fa-chevron-up" v-if="isOpen"></i>
            </transition>
          </a>
          <transition name="accordion" @before-enter="beforeEnter" @enter="enter" @before-leave="beforeLeave" @leave="leave">
            <div class="accordion-body" v-if="isOpen">
              <slot name="detail"></slot>
            </div>
          </transition>
        </div>
</template>

