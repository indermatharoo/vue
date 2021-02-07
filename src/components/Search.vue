<template>
  <div class="container-fluid">
    <div class="col-xs-12 search-section">
      <form
        class="flex-class"
        action=""
        v-on:submit.prevent="submit"
        method="post"
      >
        <div class="search-div padd-right-10">
          <div class="form-group position-relative">
            <input
              class="form-control input-search"
              type="text"
              name="search"
              placeholder="Search"
              v-on:keyup="search"
              v-model="searchText"
            />
            <span class="glyphicon glyphicon-search search-icon"></span>
          </div>
        </div>
        <div class="select-div padd-left-10">
          <div class="form-group">
            <select
              class="form-control input-select"
              @change="search"
              name="search_by"
              v-model="searchBy"
            >
              <option
                v-bind:value="searchOption.index"
                v-bind:key="searchOption.index"
                v-for="searchOption in searchOptions"
              >
                {{ searchOption.optionName }}
              </option>
            </select>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios"; // importing axios to perform http requests

// default component
export default {
  name: "Search",
  props: {},
  methods: {
    //disabling form submisstion.
    submit: function(event) {
      event.preventDefault();
    },
    // fetching right search option
    getSearchOptionFromId: function(id) {
      this.searchOptions.forEach(searchOption => {
        if (searchOption.index === id) {
          this.selectedOption = searchOption;
          return;
        }
      });
    },
    // handling cocktail search
    search: function() {
      if (this.searchText.length < 3) return;
      this.getSearchOptionFromId(this.searchBy);
      this.callServer();
    },
    // call to server for fetching records
    callServer: function() {
      const finalUrl =
        this.baseUrl +
        "/" +
        this.selectedOption.script +
        "?" +
        this.selectedOption.searchKey +
        "=" +
        this.searchText;
      // check if a request is already in process if yes stop creating another request.
      if (this.isLoading === true) return;
      this.isLoading = true;
      axios
        .get(finalUrl)
        .then(response => {
          this.$emit(
            "searched",
            response.data[this.selectedOption.responseType]
          );
        })
        .catch(error => console.log(error))
        .finally(() => (this.isLoading = false));
    }
  },
  data() {
    return {
      isLoading: false,
      baseUrl: "https://www.thecocktaildb.com/api/json/v1/1/", // base url of api
      searchBy: 1, // default search type
      searchText: "", // default search text
      selectedOption: {},
      // defining default search types
      searchOptions: [
        {
          index: 1,
          optionName: "Cocktail Name",
          searchKey: "s",
          script: "search.php",
          responseType: "drinks"
        },
        {
          index: 2,
          optionName: "Cocktail First Letter",
          searchKey: "f",
          script: "search.php",
          responseType: "drinks"
        },
        {
          index: 3,
          optionName: "Ingredient Name",
          searchKey: "i",
          script: "search.php",
          responseType: "ingredients"
        },
        {
          index: 4,
          optionName: "Cocktail Id",
          searchKey: "i",
          script: "lookup.php",
          responseType: "drinks"
        },
        {
          index: 5,
          optionName: "Ingredient Id",
          searchKey: "iid",
          script: "lookup.php",
          responseType: "ingredients"
        },
        {
          index: 6,
          optionName: "Category Name",
          searchKey: "c",
          script: "filter.php",
          responseType: "drinks"
        }
      ]
    };
  }
};
</script>

<style>
/* custom css for search box */
.input-search {
  width: 500px;
  border-radius: 20px;
  height: 40px;
  padding-left: 22px;
  font-size: 18px;
  font-weight: bolder;
}

.input-select {
  height: 40px;
}

.position-relative {
  position: relative;
}

.search-icon {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding-left: 5px;
  font-size: 12px;
}
</style>
