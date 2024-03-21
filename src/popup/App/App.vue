<template>
  <div class="main_app">
    <a href="#" @click="copyCookie">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      复制cookie 🍪
    </a>
  </div>
</template>

<script>
export default {
  name: "app",
  methods: {
    copyCookie() {
      console.log(chrome);
      chrome.tabs.query({ active: true, lastFocusedWindow: true }, (tabs) => {
        console.log(tabs);
        let url = tabs[0].url;
        console.log("url::", url, chrome);
        chrome.cookies.getAll({ domain: "jinritemai.com" }, (cookies) => {
          console.log(window.location.hostname);
          const cookieString = cookies
            .map((cookie) => `${cookie.name}=${cookie.value}`)
            .join("; ");
          console.log(cookies);
          this.copyToClipboard(cookieString);
          console.log(cookieString);
          alert("Cookie 已复制到剪贴板！");
        });
      });
    },
    copyToClipboard(text) {
      const input = document.createElement("input");
      input.style.position = "fixed";
      input.style.opacity = 0;
      input.value = text;
      document.body.appendChild(input);
      input.select();
      document.execCommand("copy");
      document.body.removeChild(input);
    },
  },
};
</script>

<style>
/*google-fonts*/

.main_app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 240px;
  color: #2c3e50;
  padding: 10px 0px;
}
body {
  background-color: #010101;
}
a {
  margin: 0 auto;
  position: relative;
  display: inline-block;
  padding: 25px 30px;
  color: #03e9f4;
  text-decoration: none;
  text-transform: uppercase;
  transition: 0.5s;
  letter-spacing: 4px;
  overflow: hidden;
}

a span {
  position: absolute;
  display: block;
}
a span:nth-child(1) {
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #03e9f4);
  animation: animate1 1s linear infinite;
}
@keyframes animate1 {
  0% {
    left: -100%;
  }
  50%,
  100% {
    left: 100%;
  }
}
a span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #03e9f4);
  animation: animate2 1s linear infinite;
  animation-delay: 0.25s;
}
@keyframes animate2 {
  0% {
    top: -100%;
  }
  50%,
  100% {
    top: 100%;
  }
}
a span:nth-child(3) {
  bottom: 0;
  right: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(270deg, transparent, #03e9f4);
  animation: animate3 1s linear infinite;
  animation-delay: 0.5s;
}
@keyframes animate3 {
  0% {
    right: -100%;
  }
  50%,
  100% {
    right: 100%;
  }
}

a span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #03e9f4);
  animation: animate4 1s linear infinite;
  animation-delay: 0.75s;
}
@keyframes animate4 {
  0% {
    bottom: -100%;
  }
  50%,
  100% {
    bottom: 100%;
  }
}
</style>
