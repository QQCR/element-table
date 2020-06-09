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
      :row-key="handleReserve"
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
          <el-image
            v-if="item.prop === 'thumb' && scope.row.thumb.length > 0"
            :src="decodeURI(scope.row.thumb[0])"
            :preview-src-list="[scope.row.thumb[0]]"
            :lazy="true"
            fit="cover"
            style="width:50px;height:40px;"
          ></el-image>
          <template v-else-if="item.tag">
            <slot name="tags" :scope="scope" :column="item.prop"></slot>
          </template>
          <span
            v-else-if="!item.isEdit"
          >{{ getText(scope.row, item.prop)}}</span>
          <!-- <el-input v-else-if="textarea[item.prop]" v-model="scope.row[item.prop]" type="textarea"></el-input> -->
          <editable-cell v-else v-model="scope.row[item.prop]" @output="changeCell" :row="scope.row" :name="item.prop">
            <span slot="content">{{scope.row[item.prop]}}</span>
          </editable-cell>
          <!-- <el-input v-else v-model="scope.row[item.prop]"></el-input> -->
        </template>
      </el-table-column>
      <!-- 如果需要自定义最后一栏则需传入operates对象,并提供模板 -->
      <el-table-column v-if="operates.operate" 
      :label="operates.label" 
      :width="operates.width"
      :align="operates.columnAlign"
      :header-align="operates.titleAlign">
        <template slot-scope="scope">
          <slot name="operates" :scope="scope"></slot>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      v-show="show_pagination"
      :current-page.sync="page"
      :page-sizes="page_list"
      :page-size="page_size"
      :total="this.total"
      layout="total,sizes, prev, pager, next, jumper"
      class="table-pagination mt-10"
      @current-change="onPageChange"
      @size-change="onSizeChange"
    />
  </div>
</template>

<script>
import EditableCell from '@/components/EditableCell';

export default {
  name: 'TablePage',
  components: {
    EditableCell
  },
  props: {
    show_pagination: {
      //是否显示分页栏
      type: Boolean,
      default: () => true
    },
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
    operates: {
      //是否增加对表行的操作功能
      type: Object,
      default: () => {
        return {
          operate: false,
          label: ''
        };
      }
    },
    list: {
      type: Array,
      default: () => null
    },
    total: {
      type: Number,
      default: () => 0
    },
    title: {
      type: Array,
      default: () => null
    },
    rowkey: {
      type: String,
      default: () => ''
    },
    pageObj: {
      type: Object,
      default: () => {
        return {
          page: 1,
          pageSize: 25,
          pageSizeList: [25, 50, 100]
        };
      }
    }
  },
  data() {
    return {
      page: 0, //分页栏当前页面
      page_size: 0, //分页栏大小,
      page_list: [],
      listQuery: {
        title: undefined,
        type: undefined
      },
      showColumns: []
    };
  },
  created() {
    this.page = this.pageObj.page;
    this.page_size = this.pageObj.pageSize;
    this.page_list = this.pageObj.pageSizeList;
  },
  watch: {
    pageObj: {
      handler: function(val) {
        this.page = val.page;
        this.page_size = val.pageSize;
      },
      deep: true
    }
  },
  methods: {
    onPageChange(page) {
      this.$emit('onPageChange', page);
    },
    onSizeChange(pagesize) {
      this.$emit('onSizeChange', pagesize);
    },
    getText(row, key) {
      return row[key];
    },
    changeCell(oldVal, newVal, row, name) {
      this.$emit('editChange',oldVal, newVal, row, name);
    },
    handleReserve(row) {
      let id = this.rowkey;
      return row[id];
    },
  }
};
</script>

