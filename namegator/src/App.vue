

<template>
  <div id="app">
    <div id="slogan" class="">
      <h1 class="text-4xl font-bold text-center text-blue-700">NameGator</h1>
      <br />
      <h6 class="text-secondary">Gerador de nomes utilizando Vue.js</h6>
    </div>
    <div id="main">
      <DomainList></DomainList>
    </div>
  </div>
</template>

<script>
import "./css/dist/tailwind.css";
import "font-awesome/css/font-awesome.min.css";
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
