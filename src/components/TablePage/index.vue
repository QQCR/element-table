<template>
  <div class="table-content">
    <el-table
      :data="list"
      class="mt-10"
      style="width: 100%"
      ref="table"
      fit
      stripe
      empty-text="暂无数据"
      :highlight-current-row="true"
    >
      <el-table-column
        v-for="(item, index) in table_title"
        :key="index"
        :prop="item.prop"
        :label="item.label"
        :width="item.width?item.width:null"
        :min-width="item.minwidth?item.minwidth:null"
        :sortable="item.sortable?item.sortable:false"
        :align="item.columnAlign"
        :header-align="item.titleAlign"
      >
        <template slot-scope="scope">
          <template v-if="item.tag">
            <slot name="tags" :scope="scope.row"></slot>
          </template>
          <span v-else>{{scope.row[item.prop]}}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'TablePage',
  props: {
    table_title: {
      //table的标题栏
      type: Array,
      default: () => [
        {
          prop: '',
          label: ''
        }
      ]
    },
    list: {
      type: Array,
      default: () => null
    },
    title: {
      type: Array,
      default: () => null
    },
    rowkey: {
      type: String,
      default: () => ''
    },
  },
  methods: {
    getText(row, key) {
      return row[key];
    },
  }
};
</script>

