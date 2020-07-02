<template>
  <div id="app">
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <br />
      <h6 class="text-secondary">Gerador de nomes utilizando Vue.js</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos
              <span class="badge badge-info">{{prefixes.length}}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li
                    class="list-group-item"
                    v-for="prefix in prefixes"
                    v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">
                        {{prefix}}
                      </div>
                      <div class="col-md text-right">                        
                        <button class="btn btn-info" v-on:click="deletePrefix(prefix)"> <span><div class="fa fa-trash"></div></span></button>  
                      </div>
                    </div>

                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input type="text" placeholder="Digite o prefixo" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" class="form-control" />
                  <div class="input-group-append">
                    <button class="btn btn-info"  v-on:click="addPrefix(prefix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>
              Sufixos
              <span class="badge badge-info">{{sufixes.length}}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{sufix}}
                      </div>
                      <div class="col-md text-right">                        
                        <button class="btn btn-info" v-on:click="deleteSufix(sufix)"> 
                          <span><div class="fa fa-trash"></div></span></button>  
                      </div>
                    </div>
                      
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input type="text" placeholder="Digite o sufixo" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" class="form-control" />
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br />
        <h5>
          Domínios
          <span class="badge badge-info">{{domains.length}}</span>
        </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">{{domain}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "font-awesome/css/font-awesome.min.css";
import "bootstrap/dist/css/bootstrap.min.css";

export default {
	name: "App",
	data: function() {
		return {
			prefix:"",
			sufix:"",
			prefixes: ["Air", "Jet", "Flight"],
			sufixes: ["Hub", "Station", "Mart"],
			domains: []
		};
	},
	methods:{
		addPrefix(prefix){
			this.prefixes.push(prefix);
			this.prefix = "";
			this.generate();
		},
		addSufix(sufix){
			this.sufixes.push(sufix);
			this.sufix = "";
			this.generate();
		},
		deletePrefix(prefix){
			this.prefixes.splice(this.prefixes.indexOf(prefix),1);
		},
		deleteSufix(sufix){
			this.sufixes.splice(this.sufixes.indexOf(sufix),1);
		},
		generate(){
			this.domains =[];
			for(const prefix of this.prefixes){
				for(const sufix of this.sufixes){
					this.domains.push(prefix+sufix);
				}
			}
		}
	},
	components: {}
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
