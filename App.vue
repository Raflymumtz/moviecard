<template>
  <body>
    <div class="header">
    <nav>
      <ul>
        <img src="./assets/home.png" img alt="home" width=20 height=20><li><a href="#">Home</a></li>
        <img src="./assets/movie.png" img alt="movie" width=20 height=20> <li><a href="#">Genre</a></li>
        <img src="./assets/cinema.png" img alt="cinema" width=20 height=20> <li><a href="#">Series</a></li>
        <img src="./assets/negara.png" img alt="negara" width=19 height=19> <li><a href="#">Country</a></li>
        <img src="./assets/tahun.png" img alt="tahun" width=20 height=20> <li><a href="#">Year</a></li> 
        <li2><a href="#"><b>MovieHunt</b></a></li2>
        <button>Search</button>
        <textbox><input type="text"></textbox>  
      </ul>
    </nav>
    </div>


  <main>
    <div class="container">
      <div class="show-list">
        <div class="show" v-for="show in shows" :key="show.show.id" >
          <img :src="show.show.image.medium" @click="showDetails(show)">
          <h2>{{show.show.name}}<p1 class="show-year">({{ new Date(show.show.premiered).getFullYear() }})</p1>
          
          </h2>
        </div>
      </div>
    </div>

    <div class="container" v-if="selectedShow">
      <div class="show-list">
        <h3>{{ selectedShow.show.name }}</h3> 
        <div class="container1">
          <img :src="selectedShow.show.image.medium">
        </div>
        <p1>{{ selectedShow.show.genres.join(', ') }}</p1>
        <p1>{{ selectedShow.show.summary}}</p1>
      </div>
    </div>
  </main>

    <footer>
      <header><a href="#"><p>&copy; 2023 MovieHunt</p></a></header>
    </footer>

  </body>
</template>

<script>
export default {
  name: 'ShowList',
  data() {
    return {
      shows: [],
      selectedShow: null,
    };
  },
  mounted() {
    fetch('http://api.tvmaze.com/search/shows?q=girls')
      .then(response => response.json())
      .then(data => {
        this.shows = data;
      });
  },
  methods: {
    showDetails(show) {
      this.selectedShow = show;
    },
  },
};
</script>

<style>
body { 
  width: 100vw;
  margin: 0;
  padding: 0;
  background-size: cover;
  object-fit: cover;
  height: 100%; 
}

img {
  border-radius: 9px;
}

main {
  background-image: url('./assets/background.jpg');
  background-size: cover;
  margin: 0px;
}

.header {
  background-color: black;
  color: #fff;
  padding: 15px;
  font-family: "sans-serif";
}

nav {
  display: left;
  justify-content: center;
}

ul {
  list-style: none;
  margin: 3px;
  padding: 0;
  display: flex;
}

li {
  margin: 0 10px;
}

li2 {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  position: absolute;
  font-size: 30px;
  margin: -9px;
}

a {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}

p1 {
  color: white;
  width: 70%;
  margin: 10px;
  text-align: center;
}

.container {
  width: auto;
  height: 86vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0px;
}

.container1 {
  width: 100%;
  height: 300px;
  display: flex;
  justify-content: center;
  top: 20px;
  
}

.card {
  width: 200px;
  height: 340px;
  margin: 30px;
  padding: 15px;
  text-align: center;
  background-color: #f5f5f5;
  border-radius:10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.card img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 10px;
}

.card h2 {
  margin: 10px 0;
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

h1 {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  position: absolute;
}

h2 {
  margin: 3px;
  font-size: 17px;
  color: white;
  justify-content: center;
  font-weight: normal;
  text-align: center;
}

h3 {
  width:100%;
  font-weight: bold;
  font-size: 40px;
  color: white;
  justify-content: center;
  display: flex;
}

label {
    display: block;
    font: 1rem 'Fira Sans', sans-serif;
}

textbox {
  position: absolute;
  right: 60px;
  width: 200px;
  height: 120px;
}

button {
  position: absolute;
  right: 20px;
  width: 60px;
  height: 21px;
}

page-container {
  position: relative;
  min-height: 100vh;
}

content-wrap {
  padding-bottom: 2.5rem; 
}

footer {
  position: sticky;
  width: auto;
  height: 2.5rem;   
  background-color: #a31818;
  padding: 10px;
  text-align: center;      
  margin-top: 0px;   
}

.show-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: flex-start;
  width: fit-content;
}

.show {
  margin: 10px;
  cursor: pointer;
}
</style>