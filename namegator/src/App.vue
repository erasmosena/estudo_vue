<template>
  <div id="app">
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br />
      <h6 class="text-secondary">Gerador de nomes utilizando Vue.js</h6>
    </div>
    <div id="main">
      <DomainList></DomainList>
    </div>
  </div>
</template>

<script>
import "font-awesome/css/font-awesome.min.css";
import "bootstrap/dist/css/bootstrap.min.css";
import DomainList from "./components/DomainList";

export default {
	name: "App",
	components: {
		DomainList
	}
};
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
