<template>
<div>
  <div class="overlay-trade-in" v-show="spinnerShow">
    <div class="w-100 d-flex justify-content-center align-items-center">
      <div class="spinner"></div>
    </div>
  </div>
  <div class="design-form">
    <h1>Testing color mode</h1>
    <div class="header-image mb-2">
    </div>
    <div class="p-3 mb-5 bg-primary text-white">.bg-primary</div>
    <span>Progress Bar </span>
    <div class="progress mb-5">
      <div class="progress-bar" role="progressbar" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
    </div>
    <form class="mb-5">
      <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
        <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
      </div>
      <div class="form-group form-check">
        <input type="checkbox" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
    <ul class="text-center">
      <li v-for="color of colors" :key="color" @click="colorChange(color)">
        {{color}}
      </li>
    </ul>
  </div>
</div>
</template>

<script>
export default {
  name: 'ColorModePicker',
  data() {
    return {
      colors: ['dark-mode', 'sepia-mode', 'default'],
      spinnerShow: true,
    }
  },
  created() {
    if(process.client) {
      this.spinnerShow = true;
      if (localStorage.getItem('colorMode')) {
        let colorType = localStorage.getItem('colorMode')
        document.getElementsByTagName('html')[0].classList.add(colorType);
      } else {
        localStorage.setItem('colorMode','default');
        document.getElementsByTagName('html')[0].className.add('test');
      }
      this.spinnerShow = false;
    }
  },
  methods: {
    colorChange(key) {
      document.getElementsByTagName('html')[0].className = '';
      document.getElementsByTagName('html')[0].classList.add(key!='default'? key : 'test');
      localStorage.setItem('colorMode', key);
    }
  }
}
</script>
<style scoped>
.design-form {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
.overlay-trade-in {
  height: 100vh;
  display: flex;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: white;
  z-index: 2;
}
.spinner {
  height: 60px;
  width: 60px;
  margin: auto;
  display: flex;
  position: absolute;
  border: 4px solid white;
  border-top: 4px solid black;
  border-radius: 100%;
  -webkit-animation: spin 1s linear infinite;
  animation: spin 1s linear infinite;
}
@keyframes spinner {
  to { transform: rotate(360deg); }
}
.spinner {
  animation: spinner 1s linear infinite;
}
</style>