<template>
<div>
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
    >
      <el-menu-item index="1">The Meal DB</el-menu-item>
    </el-menu>
    <div style="margin: 5px">
        <el-row :gutter="10" v-if="categoricalMeals.length">
            <el-col :span="6" v-for="categoricalMeal in categoricalMeals" :key="categoricalMeal.idMeal">
                <!-- card -->
                <CategoricalMeal v-bind:categoricalMeal="categoricalMeal"/>
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
import CategoricalMeal from './CategoricalMeal.vue';

export default {
    name: "Details",

    components: {
    CategoricalMeal
  },

    data() {
        return {
            categoricalMeals: [],
            loading: true,
            activeIndex: "1",
            title: this.$route.params.title
        }
    },
    methods: {
        updateMeal() {
            this.title = this.$route.params.title
        },
        handleSelect(key, keyPath) {
            console.log(key, keyPath);
        },
    },
    watch: {
        $route: 'updateMeal'
    },
    created() {
    axios
      .get("https://www.themealdb.com/api/json/v1/1/filter.php?c="+this.title)
      .then((res) => {
        this.categoricalMeals = res.data.meals;
      })
      .catch((err) => {
        console.log(err);
      });
  },
}
</script>