<template>
  <div class="table-content">
    <el-table
      :data="list"
      style="width: 100%"
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
      ></el-table-column>
    </el-table>
    <el-pagination
      :current-page.sync="pageObj.page"
      :page-sizes="pageObj.pageSizeList"
      :page-size="pageObj.pageSize"
      :total="total"
      layout="total, sizes, prev, pager, next, jumper"
      @current-change="onPageChange"
      @size-change="onSizeChange"
    />
  </div>
</template>

<script>
const table_title = [
  {
    prop: 'id',
    label: '编号',
    width: '100',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
  {
    prop: 'date',
    label: '日期',
    width: '150',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
  {
    prop: 'name',
    label: '姓名',
    width: '120',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
  {
    prop: 'province',
    label: '省份',
    minwidth: '120',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true,
    isEdit: true
  },
  {
    prop: 'city',
    label: '市区',
    minwidth: '120',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
  {
    prop: 'address',
    label: '地址',
    minwidth: '300',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
  {
    prop: 'zip',
    label: '邮编',
    minwidth: '120',
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
];

export default {
  name: 'TablePage',
  data() {
    return {
      listData: [{
          id: 1,
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333,
        }, {
          id: 2,
          date: '2016-05-04',
          name: '王小',
          province: '北京',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1517 弄',
          zip: 200333,
        }, {
          id: 3,
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1519 弄',
          zip: 200333,
        }, {
          id: 4,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 5,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 6,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 7,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 8,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 9,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }, {
          id: 10,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
        }
      ],
      table_title: table_title,
      pageObj: {
        page: 1,
        pageSize: 2,
        pageSizeList: [2, 4, 6],
      }
    }
  },
  computed: {
    total() {
      return this.listData.length
    },
    list() {
      let array = []
      this.listData.forEach((item,index) => {
        let i = Math.floor(index / this.pageObj.pageSize)
        if(!array[i]) {
           array.push([])
        }
        array[i].push(item)
      })
      return array[this.pageObj.page - 1]
    }
  },
  methods: {
    onPageChange(page) {
      this.pageObj.page = page
    },
    onSizeChange(size) {
      this.pageObj.pageSize = size
      this.pageObj.page = 1
    },
  }
};
</script>

