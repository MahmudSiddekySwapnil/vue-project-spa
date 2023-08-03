<template>
  <nav :class="[`navbar-${theme}`,`bg-${theme}`,'navbar','navbar-expand-lg']"
  >
    <div class="container-fluid">
      <div class="navbar-header">
        <a class="navbar-brand" href="#">Blog Site</a>
      </div>
      <ul class="nav navbar-nav">
        <li class="nav-item"
            v-for="(page,index) in publishedPages" :key="index">
          <navbar-link
          :page="page"
          :is-active="activePage === index"
          @click.prevent="navLinkClick(index)"
          >
          </navbar-link>
        </li>
      </ul>
      <form class="d-flex">
        <button
            class="btn btn-primary"
            @click.prevent="changeTheme()"
        >
          Toggle Nav
        </button>
      </form>
    </div>
  </nav>
</template>
<script>
import NavbarLink from "./NavbarLink.vue";
export default {
  components:{
    NavbarLink
  },
  created() {
    this.getThemeSetting();
  },
  computed:{
   publishedPages(){
     return this.pages.filter(p=>p.published);
   }
  },
  props: ['pages', 'activePage', 'navLinkClick'],
  data() {
    return {
      theme: 'light'
    }
  },
  methods: {
    changeTheme() {
      let theme = 'light';
      if (this.theme === 'light') {
        theme = 'dark';
      }
      this.theme = theme;
      this.storeThemeSetting();
    },
    storeThemeSetting(){
      localStorage.setItem('theme',this.theme);
    },
    getThemeSetting(){
      let theme = localStorage.getItem('theme');
      if(theme){
        this.theme=theme;
      }
    }
  }
}
</script>