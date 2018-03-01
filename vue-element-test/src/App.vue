<template>
<div class="custom-tree-container">
  <div class="block">
    <el-input
      placeholder="Filter keyword"
      v-model="filterText">
    </el-input>

    <el-tree
      class="filter-tree"
      v-bind:data="treeNodes"
      empty-text="No content"
      show-checkbox
      node-key="id"
      default-expand-all
      v-bind:props="defaultProps"
      v-bind:expand-on-click-node="true"
      :filter-node-method="filterNode"
      ref="tree"
      >
      <span class="custom-tree-node" slot-scope="{ node, data }">
        <span>{{ node.label }}</span>
        <span>
          <el-button type="text" size="mini" v-on:click="() => append(data)">Append</el-button>
          <el-button type="text" size="mini" v-on:click="() => remove(node, data)">Delete</el-button>
        </span>
      </span>
    </el-tree>
  </div>
</div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        treeNodes: [],
        filterText: '',
        defaultProps: {
              children: 'children',
              label: 'name'
        }
      }
    },
    watch: {
      filterText(val) {
        this.$refs.tree.filter(val);
      }
    },
    created () {
      // do something after creating vue instance
      axios.get("http://localhost:8000/api/json")
        .then((response) => {
          this.treeNodes = response.data;
        })
        .catch((error) => {
          console.log(error);
        })
    },
    methods: {
      filterNode(value, data) {
        if (!value) return true;
        return data.name.toLowerCase().indexOf(value.toLowerCase()) !== -1;
      },
      append(data) {
        console.log(data);
      },
      remove(node, data) {
        console.log(data);
      },
    }
  };
</script>

<style>
  .custom-tree-node {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 14px;
    padding-right: 8px;
  }
</style>
