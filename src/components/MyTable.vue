<template>
  <div>
    <!-- 组件内容 -->
    <el-table :data="tableData" @selection-change="handleSelectionChange" height="calc(100vh - 200px)">
      <!-- 多选 -->
      <el-table-column
        v-if="checkbox"
        type="selection"
        width="60"
      ></el-table-column>
      <el-table-column v-if="index" type="index" width="60"></el-table-column>
      <template v-for="column in columns">
        <el-table-column
          v-if="column.type === 'slot'"
          :label="column.label"
          :prop="column.prop"
          :key="column.prop"
          :width="column.width"
          :fixed="column.fixed"
          :show-overflow-tooltip="column.tooltip"
          :align="column.align"
        >
          <template slot-scope="scope">
            <slot :name="column.slot_name" :row="scope.row"></slot>
          </template>
        </el-table-column>
        <el-table-column
          v-else
          :label="column.label"
          :prop="column.prop"
          :key="column.prop"
          :width="column.width"
          :fixed="column.fixed"
          :show-overflow-tooltip="column.tooltip"
          :align="column.align"
        ></el-table-column>
      </template>
    </el-table>
    <el-pagination
      :current-page="currentPage"
      :page-sizes="pageSizes"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
    >
    </el-pagination>
  </div>
</template>

<script>
export default {
  name: "MyTable",
  data() {
    return {
      // 数据定义
    };
  },
  props: {
    tableData: {
      type: Array,
      default: [],
    },
    columns: {
      type: Array,
      default: [],
    },
    checkbox: {
      type: Boolean,
      default: false,
    },
    index: {
      type: Boolean,
      default: false,
    },
    currentPage: {
      type: Number,
      default: 1,
    },
    pageSizes: {
      type: Array,
      default: 10,
    },
    pageSize: {
      type: Number,
      default: 1,
    },
    total: {
      type: Number,
      default: 10,
    },
  },
  methods: {
    // 方法定义
    handleSelectionChange(val) {
      this.$emit("handleSelectionChange", val);
    },
  },
  created() {
    // console.log("attrs", this.$attrs);
  },
};
</script>

<style scoped>
/* 样式定义 */

::v-deep input[aria-hidden="true"] {
  display: none !important;
}
</style>
