<template>
<div class="container">
  <div class="main">
    <CardList />
  </div>
  <div class="footer">
    <FooterSite />
  </div>
</div>
</template>

<script>
import CardList from "./components/CardList.vue";
import FooterSite from "./components/FooterSite.vue";
export default {
  name: 'App',
  components:{ CardList, FooterSite },
}

</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@400;700&display=swap');
html, body{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    width: 100%;
    height: 100%;
}
h1, h2, h3, a, p{
    font-family: Nunito Sans;
}
h2, p, h1{
    color: #162841;
}
a{
    text-decoration: none;
    color: #2b4e80
}
.container{
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.footer{
  margin-top: auto
}
</style>
