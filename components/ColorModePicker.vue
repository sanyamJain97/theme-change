<template>
<div class="text-center">
  <h1>Testing color mode</h1>
    <ul>
      <li v-for="color of colors" :key="color" @click="colorChange(color)">
        {{color}}
      </li>
    </ul>
</div>
</template>

<script>
export default {
  name: 'ColorModePicker',
  data() {
    return {
      colors: ['dark-mode', 'sepia-mode']
    }
  },
  methods: {
    colorChange(key) {
        document.getElementsByTagName('html')[0].className = '';
        document.getElementsByTagName('html')[0].classList.add(key);
    }
  }
}
</script>
