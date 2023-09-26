<template>
  <el-row>
    <el-card class="boxcard">
      <el-row class="age">
        <el-col>
          <h1>AGE CALCULATOR</h1>
        </el-col>
      </el-row>
      <el-row class="dateLable">
        <el-col :span="8">DD</el-col>
        <el-col :span="8">MM</el-col>
        <el-col :span="8">YY</el-col></el-row>
      <el-row :gutter="10" class="date">
        <el-col :span="8" label="Name">
          <el-input v-model="base.date.day" size="large" placeholder="Enter a Day" /></el-col>
        <el-col :span="8"><el-input v-model="base.date.month" size="large" placeholder="Enter a Month" /></el-col>
        <el-col :span="8"><el-input v-model="base.date.year" size="large" placeholder="Enter a year" /></el-col>
      </el-row>
      <el-row class="get">
        <el-button type="danger" @click="getClearAge">Clear</el-button>
        <el-button type="success" @click="getCurrentAge">Click & Get</el-button>
      </el-row>

      <el-row v-if="base.getDate" class="dateLable">
        <el-col>
          <h2 style="color: rgb(241, 9, 179)">
            {{ `AGE IS = ${base.y} YEAR ${base.m} MONTH ${base.d} DAYS OLD` }}
          </h2>
        </el-col>
      </el-row>
    </el-card>
  </el-row>
</template>

<script>
import { ElMessage } from "element-plus"
import { reactive } from "vue";
export default {
  name: "AgeCalculator",
  setup() {
    let base = reactive({
      date: {
        day: "",
        month: "",
        year: "",
      },
      d: "",
      m: "",
      y: "",
      getDate: false,
    });

    const getCurrentAge = () => {
      if (base.date.day && base.date.month && base.date.year) {
        let date = new Date();
        let d2 = date.getDate();
        let m2 = 1 + date.getMonth();
        let y2 = date.getFullYear();
        console.log("date", date);
        let month = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
        if (base.date.day > d2) {
          d2 = d2 + month[m2 - 1];
          m2 = m2 - 1;
        }
        if (base.date.month > m2) {
          m2 = m2 + 12;
          y2 = y2 - 1;
        }
        base.d = d2 - base.date.day;
        base.m = m2 - base.date.month;
        base.y = y2 - base.date.year;
        base.getDate = true;
        console.log("base.d", base.d, "base.m", base.m, "base.y", base.y);
      }
      else {
        ElMessage({
          message:'FILL THE FIELDS.',
          type:'error'
        })

      }

    };
    const getClearAge = () => {
      base.getDate = false;
      base.date = {
        day: "",
        month: "",
        year: "",
      };
    };
    return {
      base,
      getCurrentAge,
      getClearAge,
    };
  },
};
</script>

<style>
@media (max-width:800px) and (min-width: 200px) {
  .boxcard {
    height: 320px;
    width: 380px;
    margin-left: 12px;
    background-color: aqua;
  }

  .boxcard .get {
    margin-top: 20px;
    margin-left: 90px;
  }
}
</style>
