<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <AppItemList
              v-bind:items="prefixes"
              title="Prefixos"
              v-on:addItem="addPrefix"
              v-on:deleteItem="deletePrefix"
            ></AppItemList>
          </div>
          <div class="col-md">
            <AppItemList
              v-bind:items="sufixes"
              title="Sufixos"
              v-on:addItem="addSufix"
              v-on:deleteItem="deleteSufix"
            ></AppItemList>
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
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                <div class="row">
                  <div class="col-md">{{domain.name}}</div>
                  <div class="col-md text-right">
                    <a v-bind:href="domain.checkout" target="_blank" class="btn btn-info">
                      <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


import AppItemList from "./AppItemList";
import axios from "axios/dist/axios";

export default {
	name: "DomainList",
	components: {
		AppItemList
	},
	data: function() {
		return {
			prefixes: ["Air", "Jet", "Flight"],
			sufixes: ["Hub", "Station", "Mart"]
		};
	},
	methods: {
		addPrefix(prefix) {
			//this.prefixes.push(prefix);
			axios({
				url:"http://localhost:4000",
				method:"post",
				data:{
					query: `
						mutation($item:ItemInput){
							newPrefix: saveItem(item: $item){
								id
								type
								description
							}
						}
					`,
					variables:{
						item:{
							type:"prefix",
							description: prefix
						}
					}
				}
			}).then((response)=>{
				const query = response.data;
				const newPrefix = query.data.newPrefix;
				this.prefixes.push(newPrefix.description);
			});
			
		}, 

		addSufix(sufix) {
			this.sufixes.push(sufix);
			this.sufix = "";
		},

		deletePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},

		deleteSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		},

		getPrefixes(){
			axios({
				url:"http://localhost:4000",
				method:"post",
				data:{
					query: `
						{
							prefixes: items( type: "prefix") {
								id
								type
								description
							}
						}
					`
				}
			}).then((response)=> {
				const query = response.data;
				this.prefixes = query.data.prefixes.map(it=>it.description);				
			});
		},

		
		getSufixes(){
			axios({
				url:"http://localhost:4000",
				method:"post",
				data:{
					query: `
						{
							sufixes: items( type: "sufix") {
								id
								type
								description
							}
						}
					`
				}
			}).then((response)=> {
				const query = response.data;
				this.sufixes = query.data.sufixes.map(it=>it.description);
				console.log(query);
			});
		}
	},
	computed: {
		domains() {
			console.log("generating");
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					const name = prefix + sufix;
					const url = name.toLowerCase();
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
					domains.push(
						{
							name,
							checkout
						}
					);
				}
			}
			return domains;
		}
	},
	created(){
		this.getPrefixes();
		this.getSufixes();
	}
};
</script>

<style>
</style>
