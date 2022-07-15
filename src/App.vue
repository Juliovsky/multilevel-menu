<template>
  <div>
  <div id="app">
    <div class="title">
      <div class="-t">Italian Restaurant</div>
      <div class="-c">Peter Pizza</div>
      <div class="-b">Bon Appetit !</div>
    </div>
    <div class="content">
      <MultilevelMenu
          :menu="menu"
      />
    </div>
  </div>
  <div id="modals"></div>
  </div>
</template>

<script>
import MultilevelMenu from "@/components/MultilevelMenu.vue";
import menuData from "@/menu.json";

export default {
  name: "app",
  components: {
    MultilevelMenu,
  },
  data() {
    return {
      menu: menuData,
    };
  }
};
</script>

<style>

body {
  display: flex;
  justify-content: center;
  /*align-items: center;*/
  width: 100%;
  height: 100vh;
  margin: 0;
  padding: 0;
  background: #000;
  color: #fff;
  font-family: -apple-system,BlinkMacSystemFont,'Roboto','Helvetica Neue',Geneva,"Noto Sans Armenian","Noto Sans Bengali","Noto Sans Cherokee","Noto Sans Devanagari","Noto Sans Ethiopic","Noto Sans Georgian","Noto Sans Hebrew","Noto Sans Kannada","Noto Sans Khmer","Noto Sans Lao","Noto Sans Osmanya","Noto Sans Tamil","Noto Sans Telugu","Noto Sans Thai",sans-serif,arial,Tahoma,verdana;
}

.title {
  display: inline-block;
  transform: skewY(-5deg);
  font-size: calc(40vw / 5);
  white-space: nowrap;
  line-height: 1.15;
}

.title .-t,
.title .-b {
  font-size: 25%;
  font-weight: 200;
  text-transform: lowercase;
}

.title .-c {
  display: block;
  --gradient: linear-gradient(80deg, #8bfd50, #66f6ff);
  background-image: var(--gradient);
  background-clip: text;
  /* for stupid WEBKIT -_- */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
  /* for stupid WEBKIT -_- */
  color: transparent;
  position: relative;
  text-align: center;
  margin: .05em 0;
  padding: .05em 0;
  font-weight: 900;
  position: relative;
}

.title .-c::before,
.title .-c::after {
  content: '';
  display: block;
  width: 100%;
  height: 100%;
  background-image: var(--gradient), var(--gradient);
  background-repeat: no-repeat;
  background-position: top left, bottom left;
  background-size: auto .05em;
  position: absolute;
  top: 0;
  left: 0;
}

.title .-c::before {
  filter: blur(5px);
  z-index: 1;
}

.title .-c::after {
  z-index: 2;
  /* for stupid WEBKIT -_- */
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  filter: blur(.025px);
  /* for stupid WEBKIT -_- */
}

.title .-b {
  text-align: right;
}

.content {
  margin-top: 70px;
}
</style>
