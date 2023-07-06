<template>
  <div id="app">
    <header>
      <nav>
        <div class="wrapper">
          <img src="./assets/Logo.png" alt="Logo" />
          <div class="logo1"><h2>idget.</h2></div>
        </div>
        <div class="menu">
          <ul>
            <li><router-link to="/">Weather</router-link></li>
            <li><router-link to="/location">Location</router-link></li>
            <li><router-link to="/stopwatch">Stopwatch</router-link></li>
            <li><router-link to="/tictactoe">Tic Tac Toe</router-link></li>
            <li><router-link to="/photo" class="tombol1">Photo</router-link></li>
          </ul>
        </div>
      </nav>
    </header>
    <router-view></router-view>
  </div>
  <div id="copyright">
    <div class="cp">
      &copy; 2023. <b>Widget.</b>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  text-decoration: none;
  margin: 0px;
  padding: 0px;
  font-family: 'Open Sans',sans-serif;
}

.wrapper{
  display: flex;
  align-items: center;
}

.wrapper img {
  width: 150px; 
  height: 150px; 
  margin-right: -34px;
  border-radius: 50%;
}

.logo1 h2 {
  font-size: 50px;
  font-weight: 800;
  float: left;
  font-family: courier;
  color: #000000;
}

.menu a {
  float: right;
  font-size: 20px;
}

header {
  background: #ffffff;
  padding: 20px;
  margin-top: -25px;
}

nav {
  width: 100%;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  line-height: 20px;
  position: sticky;
  position: -webkit-sticky;
  top: 0;
  background-color: #ffffff;
  z-index: 1;
  border-bottom: 5px solid #ff0000;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  display: flex;
}

nav li {
  float: left;
  margin-right: 10px;
}

nav ul li a {
  color: black;
  font-weight: bold;
  text-align: center;
  padding: 5px 10px;
  text-decoration: none;
}

nav ul li a:hover {
  text-decoration: underline;
  color: rgb(252, 50, 50);
}

.tombol1 {
    background: rgb(252, 50, 50);
    border-radius: 10px;
    margin-top: 0px;
    padding: 5px 20px 5px 20px;
    color:#FFFFFF;
    cursor: pointer;
    font-weight: bold;
}

.tombol1:hover {
    background: rgb(255, 112, 112);
    color: #d1cfcf;
    text-decoration: none;
}

#copyright {
  text-align: center;
  width: 100%;
  padding: 50px 0px 50px 0px;
  margin-top: 50px;
}

.cp{
    width: 1100px;
    margin: auto;
    position: relative;
}

</style>
