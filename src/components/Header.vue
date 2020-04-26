<template>
    <nav class="navbar navbar-default">
     <div class="container-fluid"> 
       <div class="navbar-header">
  <router-link to="/" class="navbar-brand">Stock Brocker</router-link>
     </div>

  <div class="collapse navbar-collapse" >
    <ul class="nav navbar-nav ">
      <router-link to="/portfolio" activeClass="active" tag="li">
        <a>Portfolio</a>
      </router-link>
      <router-link to="/stocks" activeClass="active" tag="li">
        <a>Stocks</a>
      </router-link>
    </ul>
    <strong class="navbar-text navbar-right">Funds: {{funds | currency}}</strong>
    <ul class="nav navbar-nav navbar-right ">
      <li class="nav-item">
        <a href="#" @click="endDay">End Day</a>
        </li>
      <li class="nav-item dropdown"
       :class="{open: isDropdownOpen}"
       @click="isDropdownOpen = !isDropdownOpen">
        <a 
        class=" dropdown-toggle" 
        href="#" 
        id="navbarDropdown" 
        role="button" 
        data-toggle="dropdown" 
        aria-haspopup="true" 
        aria-expanded="false">
          Save & Load
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <li><a class="dropdown-item nav-link" href="#" @click="saveData">Save Data</a></li>
          <li><a class="dropdown-item nav-link" href="#" @click="loadData" >Load Data</a></li>
        </div>
      </li>
    </ul>
  </div>
  </div>
</nav>
</template>

<script>
import {mapActions} from 'vuex';

export default {
  data(){
    return{
      isDropdownOpen: false
    }
  },
  computed: {
    funds(){
      return this.$store.getters.funds;
    }
  },
    methods:{
      ...mapActions({
        randomizeStocks: 'randomizeStocks',
        fetchData: 'loadData'
      }),
      endDay(){
        this.randomizeStocks();
      },
      saveData(){
        const data = {
          funds: this.$store.getters.funds,
          stockPortfolio: this.$store.getters.stockPortfolio,
          stocks: this.$store.getters.stocks
        };
        this.$http.put('data.json', data);
      },
      loadData(){
        this.fetchData();
      }
    }
  
}
</script>