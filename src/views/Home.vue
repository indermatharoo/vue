<template>
  <div id="warp">
    <div class="contents">
      <div class="outer-background">
        <div class="inner-background">
          <!-- handling emit event  -->
          <Search v-on:searched="updateSearchResults" />
          <!-- passing data to child component  -->
          <List :searchResults="this.searchResults" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Search from "@/components/Search.vue"; // including search component
import List from "@/components/List.vue"; // including list component

export default {
  name: "Home",
  components: {
    Search,
    List
  },
  methods: {
    // updating search results
    updateSearchResults: function(response) {
      this.searchResults = response;
    }
  },
  data() {
    return {
      searchResults: []
    };
  }
};
</script>

<style>
/* custom css */
* {
  margin: auto 0;
  padding: 0;
}
body {
  font-family: "Roboto", sans-serif;
  background: #eeeeee;
}
a {
  color: #000000;
}

a:hover {
  color: #000000;
  text-decoration: none;
}

.flex-class {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
}

.padd-right-10 {
  padding-right: 10px;
}

.padd-left-10 {
  padding-left: 10px;
}

.search-section {
  padding: 40px 0px 30px 0px;
}

.dot {
  height: 50px;
  width: 50px;
  background-color: #42a5f6;
  border-radius: 50%;
  display: inline-block;
}

.title-sec {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  padding: 20px 0px 15px 0px;
}

.padd-left-15 {
  padding-left: 15px;
}

.inner-background {
  background: #ffffff;
}

.outer-background {
  background: #eeeeee;
  padding: 50px;
}
/* Media query started */

@media (min-width: 1400px) {
  .container-fluid {
    width: 1366px;
  }
}

@media (min-width: 1500px) {
  .col-4-padd {
    padding: 0px 50px 0px 50px;
    margin-top: 25px;
  }
  .container-fluid {
    width: 1400px;
  }
}

@media (min-width: 1900px) {
  .container-fluid {
    width: 1800px;
  }
}
@media (min-width: 2200px) {
  #warp {
    position: relative;
    min-height: 100vh;
  }
  .contents {
    position: absolute;
    right: 0;
    left: 0;
    margin: auto 0;
    top: 50%;
    transform: translateY(-50%);
    border: 0;
  }
}

@media (min-width: 0px) and (max-width: 768px) {
  .col-xs-4 {
    width: 100%;
  }
  .input-search {
    width: 100%;
  }
  .title-sec {
    flex-wrap: unset;
  }
  .desc-buttons {
    margin: 0 auto;
  }
  .open {
    padding: 0px 10px 0px 10px;
  }
  .share {
    padding: 0px 10px 0px 10px;
  }
  .description-sec > .desc {
    padding: 26px 9px 20px 10px;
  }
  .padd-left-15 {
    padding-left: 10px;
  }
  .responsive-padd-top-80 {
    padding-top: 80px;
  }
  .col-4-padd {
    margin-top: 20px;
    padding: 0px 80px;
  }
}
/* Media query ended */
</style>
