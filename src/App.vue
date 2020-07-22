<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

header {
    display: flex;
    flex-direction: row;
    padding: 10px 20px;
    background: #484848;
    box-shadow: 0 9px 16px 0 rgba(0,0,0,0.37);
}
header h1 {
  font-size: 35px;
  color: #FFFFFF;
  letter-spacing: 0;
}
header .arrow {
  margin-right: 30px;
  cursor: pointer;
}
</style>
