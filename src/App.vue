<template>
  <div id="container" >
    <!-- ADD COMPLEMENT -->
    <add-complement></add-complement> 

    <!-- SHOW EXPERIENCE -->
    <show-experience></show-experience> 
  </div>
</template>

<script>
import AddComplement from './components/AddComplement.vue';
import ShowExperience from './components/ShowExperience.vue';

export default {
  components: {
    AddComplement,
    ShowExperience,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');

body {
  background: #FEAC5E;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #4BC0C8, #C779D0, #FEAC5E);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #4BC0C8, #C779D0, #FEAC5E); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  text-align: center;
  font-family: 'Varela Round', sans-serif;
}
#container {
  max-width: 1440px;
  margin: auto;
}

</style>