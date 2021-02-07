<template>
  <section id="content-section">
    <div class="container-fluid">
      <div
        class="col-xs-4 col-4-padd"
        :key="index"
        v-for="(searchResult, index) in searchResults"
      >
        <div class="item box-shadow">
          <div class="title-sec">
            <div class="blue-circle padd-left-15">
              <span class="dot"></span>
            </div>
            <div class="product-name padd-left-15">
              <span class="title">
                {{
                  searchResult.strDrink
                    ? searchResult.strDrink
                    : searchResult.strIngredient
                }} </span
              ><br />
              <span>
                {{ searchResult.strCategory }}
              </span>
            </div>
          </div>
          <div class="img-section" v-if="searchResult.strDrinkThumb">
            <div class="img-div">
              <img
                class="img-responsive display-initial"
                v-bind:src="searchResult.strDrinkThumb"
                alt="Product Alt"
              />
            </div>
          </div>
          <div class="description-sec">
            <div class="desc">
              {{
                searchResult.strInstructions.length > 40
                  ? searchResult.strInstructions.substring(0, 40) + " ..."
                  : searchResult.strInstructions
              }}
            </div>
            <div class="desc-buttons">
              <div class="open">
                <a href="javascript:void(0)">
                  open
                </a>
              </div>
              <div class="share">
                <a href="javascript:void(0)">
                  share
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// default component
export default {
  name: "List",
  props: ["searchResults"],
  data() {
    return {};
  }
};
</script>

<style>
/* custom css for listing page */
.img-section {
  background: #e3f2f9;
  text-align: center;
}

.title {
  font-weight: 600;
}

.display-initial {
  display: initial !important;
  width: 200px;
}

.description-sec > .desc {
  padding: 26px 15px 20px 20px;
  font-size: 15px;
}

.desc-buttons {
  text-transform: uppercase;
  display: flex;
  align-items: center;
  padding: 20px 0px 20px 20px;
  font-weight: 500;
}

.open {
  padding: 0px 30px 0px 30px;
}

.share {
  padding: 0px 30px 0px 30px;
}

.box-shadow {
  -moz-box-shadow: 0px 9px 5px 6px #ccc;
  -webkit-box-shadow: 0px 9px 5px 6px #ccc;
  box-shadow: 0px 9px 5px 6px #ccc;
}

.second-col {
  padding: 80px 15px 40px 15px;
}
</style>
