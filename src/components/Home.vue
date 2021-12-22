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
    <div>
        <AllMeals />
    </div>
  </div>
</template>

<script>
import AllMeals from "./AllMeals.vue";

export default {
  name: "Home",
  components: {
    AllMeals,
  },
  data() {
    return {
      activeIndex: "1",
    };
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
  },
};
</script>