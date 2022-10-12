<template>
  <div class="router-link-container">
    <router-link class="router-link" to="/">Pokemon Picker</router-link>
  </div>
  <router-view/>
</template>

<style>
  .router-link-container{
    margin-top: 30px;
    margin-bottom: 50px;
  }

  .router-link{
    display: flex;
    justify-content: center;
    font-size: xx-large;
    font-weight: 700;
    color: rgb(255, 187, 0);
    text-decoration: none;
  }  

  html{
    background-color: rgba(238, 186, 234, 0.393);
    font-family:'Gill Sans', 'Gill Sans MT', 'Trebuchet MS', sans-serif
  }
</style>
