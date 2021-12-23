<template>
  <div>
    <el-container id="searchHeader">
      <h3 id="searchHeading">Search Your Favourite Meals</h3>
      <el-aside width="200px">
        <el-input placeholder="Search here" v-model="searchInput"></el-input>
      </el-aside>
      
    </el-container>
    <div>
      <el-row :gutter="10" v-if="meals.length">
        <el-col :span="6" v-for="meal in filterSearch" :key="meal.idCategory">
          <!-- card -->
          <Meal v-bind:meal="meal"/>
        </el-col>
      </el-row>
      <div v-else id="loadingAnimation">
        <div v-loading="loading"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Meal from './Meal.vue';

export default {
  name: "AllMeals",

  // props: [
  //   'title','url'
  // ],

  components: {
    Meal
  },

  data() {
    return {
      meals: [],
      loading: true,
      searchInput: '',
    };
  },
  computed: {
    filterSearch() {
      return this.meals.filter(meal => {
        return meal.strCategory.toLowerCase().match(this.searchInput)
      })
    }
  },
  created() {
    axios
      .get("https://www.themealdb.com/api/json/v1/1/categories.php")
      .then((res) => {
        console.log(res);
        this.meals = res.data.categories;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style>
#searchHeading {
  margin-right: 10px
}
#searchHeader {
  text-align: center;
  align-items: center;
  justify-content: center;
  margin: 5px;
  padding: 10px;
  color: #67c23a;
}
.el-row {
  margin-bottom: 20px;
  /* &:last-child {
      margin-bottom: 0;
    } */
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple-light {
  background: #e5e9f2;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
#loadingAnimation {
  margin-top: 200px;
}
</style>