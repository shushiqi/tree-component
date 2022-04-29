<template>
  <div class="tree-node-wrapper">
    <div class="tree-item" v-for="(item, index) in cloneData" :key="index">
      <div class="tree-main" @click="show(index)">
        <div class="tree-icon" v-if="item.children && item.children.length">
          {{ item.expand ? "-" : "+" }}
        </div>
        <div class="tree-icon" v-else>&nbsp;&nbsp;</div>
        <div class="tree-content">{{ item.label }}</div>
      </div>
      <div
        class="tree-children"
        v-if="item.children && item.children.length"
        v-show="item.expand"
      >
        <tree-node :data="item.children"></tree-node>
      </div>
    </div>
  </div>
</template>

<script>
import deepClone from "../utils/deepClone";
export default {
  name: "TreeNode",
  props: {
    data: {
      default: () => [],
      type: Array,
    },
  },
  data() {
    return {
      showChildren: false,
      cloneData: [],
    };
  },
  created() {
    this.cloneData = deepClone(this.data);
  },
  methods: {
    show(index) {
      this.$set(this.cloneData[index], "expand", !this.cloneData[index].expand);
    },
  },
};
</script>

<style scoped>
.tree-wrapper {
  width: 100%;
}

.tree-item {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
}

.tree-main {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  cursor: pointer;
}

.tree-icon {
  margin: 0 0.2rem;
}

.tree-children {
  width: 100%;
  margin-left: 2rem;
}
</style>
