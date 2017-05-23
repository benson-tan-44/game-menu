<template>
  <nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <router-link class="navbar-brand" to="/">Game Menu</router-link>
    </div>

    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <router-link to="/inventory" activeClass="active" tag="li"><a>Inventory</a></router-link>
        <router-link to="/store" activeClass="active" tag="li"><a>Store</a></router-link>
        <router-link to="/party" activeClass="active" tag="li"><a>Party</a></router-link>
      </ul>
        <strong class="navbar-text navbar-right">Funds: {{funds}} </strong>
      <ul class="nav navbar-nav navbar-right">
      <li :class="{open: isDropdownOpen}" class="dropdown">
        <a
        href="#"
        class="dropdown-toggle"
        data-toggle="dropdown"
        role="button"
        aria-haspopup="true"
        @click="isDropdownOpen = !isDropdownOpen"
        aria-expanded="false">Save & Load <span class="caret"></span></a>
        <ul class="dropdown-menu">
          <li><a @click="saveGame" href="#">Save Game</a></li>
          <li><a @click="loadGame" href="#">Load Game</a></li>
        </ul>
        </li>
      </ul>


    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
  data(){
    return {
      isDropdownOpen: false
    }
  },
  computed: {
    ...mapGetters({
      funds: 'funds'
    })
  },
  methods: {
    saveGame(){
      const data = {
        funds: this.$store.getters.funds,
        items: this.$store.getters.items,
        party: this.$store.getters.party
      };
      this.$http.put('data.json', data);
      this.isDropdownOpen = false;
    },
    loadGame() {
      this.$store.dispatch('loadData');
      this.isDropdownOpen = false;

    }
  }

}

</script>
