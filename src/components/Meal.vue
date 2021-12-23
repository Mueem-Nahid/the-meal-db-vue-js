<template>
  <div class="grid-content bg-purple">
    <el-card :body-style="{ padding: '10px' }">
      <img v-bind:src="meal.strCategoryThumb" class="image" />
      <div style="padding: 14px">
        <span>{{meal.strCategory}}</span>
        <div class="bottom clearfix">
          <el-button type="text" class="button">View</el-button>
        </div>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  props: {
    meal: Object,
  }  
}
</script>

<style>
.bottom {
  margin-top: 13px;
  line-height: 12px;
}
.button {
  padding: 0;
}
.image {
  width: 100%;
  display: block;
}
.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
  text-align: center;
}
.bg-purple {
  background: #d3dce6;
}
</style>