<template>
  <div>
    <h3 id="searchHeader">Search Your Favourite Meals</h3>
    <div>
      <el-row>
        <el-col
          :span="8"
          v-for="meal in meals"
          :key="meal.idCategory"
        >
          <el-card :body-style="{ padding: '0px' }">
            <img
              v-bind:src="meal.strCategoryThumb"
              class="image"
            />
            <div style="padding: 14px">
              <span>{{meal.strCategory}}</span>
              <div class="bottom clearfix">
                <el-button type="text" class="button">View</el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AllMeals",
  data() {
    return {
      meals: [],
    };
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

<style scoped>
#searchHeader {
  text-align: center;
  margin: 10px;
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
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
</style>