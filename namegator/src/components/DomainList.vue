<template>
  <div >
    <div id="main">
      <div class="w-full max-w-xs">
        <div class="flex flex-wrap">          
            <AppItemList v-bind:items="prefixes" title="Prefixos" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix"></AppItemList>                      
            <AppItemList v-bind:items="sufixes" title="Sufixos" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix"></AppItemList>                      
        </div>
        
        <h5>
          Domínios
          <span >{{domains.length}}</span>
        </h5>
        <div >          
            <ul >
              <li v-for="domain in domains" v-bind:key="domain.name">                
                  <div >{{domain.name}}</div>
                  <div >                    
                    <a v-bind:href="domain.checkout" target="_blank" >
                    <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>                
              </li>
            </ul>
        
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import "font-awesome/css/font-awesome.min.css";
import AppItemList from "./AppItemList";

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
			this.prefixes.push(prefix);
			this.prefix = "";
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
	}
};
</script>

<style>

</style>
