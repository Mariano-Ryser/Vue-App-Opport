<template>
  <div id="app">
    <!-- title -->
     <h1 class="site-title">{{title}}</h1>
      
      <span class="site-description">{{ currentDate }}</span>


       <!-- entry list -->
     <ul v-on:click="tuca()" class = "entry-list"> 
       <li 
          class="entry-item"
          v-for="entry in filteredEntries"
          :key="entry.id"
          >

         <span class="entry-daytime">{{entry[0]}} Uhr - {{entry[1].replaceAll("/",".")}} </span>
         <h3 class="entry-title">{{entry[2]}}</h3>
         <span class="entry-description">{{entry[3]}}</span> <br>
         <span class="entry-description-extra">{{entry[4]}}</span> 
     
         
       </li>
     </ul>
     
   <footer class="footer">
     
   </footer>

  </div>
</template>


<script>
import axios from "axios";

export default {
   name: "App",
  data(){
    return {
      title: "Mariano N. Ryser",
      currentDate: "",
      gsheet_url: 
        "https://sheets.googleapis.com/v4/spreadsheets/1_N4YuujKyEpU2bgKr0dlA1jOZ-m31zGqZdD7WCaO0XY/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=AIzaSyBsnFNbHQWLcYlyEmCpOuL2lHZBwFyzDGw",
      entries : [],
    };
  }, // <----- data ende
  computed :{
    filteredEntries() {
      return [...this.entries].slice(1); // remove first item of array
    },
  },// <----- computed properties are like data properties, but with a method combined, it gets executed automatically, instead of calling a function explicitly
  methods: {
    tuca(){
      alert('Auch ein test');
    },
    getData(){
      axios.get(this.gsheet_url).then((response) => {
      this.entries = response.data.valueRanges[0].values;
      })
    },
    updataCurrentDate(){
      let today = new Date();
      const date = `${today.getDate()}.${today.getMonth() + 1 }.${today.getFullYear()}`;
      this.currentDate = date;
    },
    refreshData() {
      this.getData();
      this.updataCurrentDate();
      }
  }, // <----- methods ende
  mounted(){
    this.refreshData();   // get first intitial data and then wait for the next update

    setInterval(() => {
      this.refreshData();
    }, 1800000) // wait 30min for next update
  }       // <----- mounted ende
};      // <----- export default ende
</script>

<style>
@import url(https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22%22);

body {
  background-color:yellow;
}

#app {
  font-family: "Inter", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 20px;
  color: black;
}

.site-title {
  font-size: 70px;
  font-weight: 900;
  margin: 20px 0px 20px 0px;
}


.site-description {
  font-size: 62px;
  color: black;
  margin: 0;
  color: #323d4a;

}

.entry-list {
  padding-left: 0;
}

.entry-item {
  
  padding: 25px 30px;
  margin: 20px 0;
  font-size: 28px;
  line-height: 1.3;
  list-style: none;
  /*background: #0f05a0;*/
  transition: 0.5s;
  border: 5px dashed black;
  animation: bord 100s infinite alternate ease-out;
}
@keyframes bord{
  0%{
    background:yellow;
  }
  100%{
    background:green;
  }
}
/* MEDIA QUERI */


.entry-daytime {
  font-weight: 900;
  color:black;
}

.entry-title {
  font-size: inherit;
  font-weight: 900;
  color:black;
  margin: 0;
}

.entry-description {
  font-weight: 500;
  color:black;
}

.entry-description-extra{
  font-weight: 400;
  color:black;
}

.footer {
  display: flex;
  flex-direction:column;
  padding: 50px;
  box-sizing: border-box;
  background-color:yellow;
  border: 5px dashed black;
  bottom: 0;
  left: 0;
  width: 100%;
}

.footer img {
  height: 50px;
}


/* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI */
/* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI */
/* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI */
/* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI */
/* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI *//* MEDIA QUERI */


@media (max-width: 600px) {
body {
  background: #e8eff4;
}

#app {
  font-family: "Inter", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 10px;
  color: #323d4a;
}

.site-title {
  font-size: 60px;
  font-weight: 900;
  margin: 20px 0 0px 0;
}
.box-foto-info{
  display:grid;
  grid-template-columns: auto;
}
.foto{
 height:340px;
 border-radius:20%;
}
.site-description {
  font-size: 42px;
  color: #323d4a;
  margin: 0;
}


.entry-list {
  padding-left: 0;
}

.entry-item {
  cursor: pointer;
  padding: 35px 40px;
  margin: 40px 0;
  font-size: 28px;
  line-height: 1.3;
  list-style: none;
  background: #0f05a0;
  transition: 0.5s;
}

.entry-item:hover {
  background: #4f7ebd;
  box-shadow: rgb(0, 0, 0) 10px 10px 70px;
}

.entry-daytime {
  font-weight: 900;
  color: #eb5e00;
}

.entry-title {
  font-size: inherit;
  font-weight: 900;
  color: #ffbfab;
  margin: 0;
}

.entry-description {
  font-weight: 500;
  color: #ffbfab;
}

.entry-description-extra{
  font-weight: 400;
  color: #ffbfab;
}

  .footer {
  display: flex;
  flex-direction:column;
  padding: 20px;
  box-sizing: border-box;
  background-color:yellow;

  bottom: 0;
  left: 0;
  width: 100%;
}
  .footer img {
  height: 35px;
  padding: 20px;

}
}



</style>