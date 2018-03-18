<template>
  <el-tabs v-model="plansValue" type="card" editable @edit="handleTabsEdit">
    <el-tab-pane
      :key="item.index"
      v-for="(item, index) in plans"
      :label="item.title"
      :name="item.name"
    >
        <el-form-item
      props="plans"
      :rules="plansRule"
    >
      <component :is="item.content" v-model="item.data" :index="index"></component>
    </el-form-item>

    </el-tab-pane>
  </el-tabs>
</template>

<script>
import PlanForm from "./PlanForm";
import planDataConstructor from "./plan.js";

export default {
  components: {
    PlanForm
  },
  data() {
    return {
      plansRule: [{ type: "number", message: "年龄必须为数字值" }],
      plansValue: "1",
      tabIndex: 1
    };
  },
  model: {
    prop: "plans",
    event: "change"
  },
  props: {
    plans: {
      type: Array
    }
  },
  methods: {
    addTab() {
      let newTabName = ++this.tabIndex + "";
      this.plans.push({
        title: "New Tab" + this.tabIndex,
        name: newTabName,
        content: PlanForm,
        data: planDataConstructor()
      });
      this.plansValue = newTabName;
    },
    removeTab(targetName) {
      let tabs = this.plans;
      let activeName = this.plansValue;
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1];
            if (nextTab) {
              activeName = nextTab.name;
            }
          }
        });
      }

      this.plansValue = activeName;
      this.plans = tabs.filter(tab => tab.name !== targetName);
    },
    handleTabsEdit(targetName, action) {
      if (action === "add") {
        this.addTab();
      }
      if (action === "remove") {
        this.removeTab(targetName);
      }
    }
  }
};
</script>

<style scoped>

</style>
