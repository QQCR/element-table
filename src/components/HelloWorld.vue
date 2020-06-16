<template>
  <div>
    <table-page
      :list="listData"
      :table_title="table_title"
    >
      <template v-slot:tags="scope">
        <el-tag
          v-if="scope.scope.tag == 1"
          size="small"
          type="primary"
          >tag1
        </el-tag>
        <el-tag
          v-else-if="scope.scope.tag == 2"
          size="small"
          type="warning"
          >tag2
        </el-tag>
        <el-tag
          v-else-if="scope.scope.tag == 3"
          size="small"
          type="success"
          >tag3
        </el-tag>
      </template>
    </table-page>
  </div>
</template>

<script>
import TablePage from '@/components/TablePage'

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
    prop: 'auditflag',
    label: '状态',
    minwidth: '80px',
    tag: true,
    titleAlign: 'center',
    columnAlign: 'center',
    sortable:true
  },
];


export default {
  components: {
    TablePage,
  },
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
          tag: "1"
        }, {
          id: 2,
          date: '2016-05-04',
          name: '王小',
          province: '北京',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1517 弄',
          zip: 200333,
          tag: "2"
        }, {
          id: 3,
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1519 弄',
          zip: 200333,
          tag: "3"
        }, {
          id: 4,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "1"
        }, {
          id: 5,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "2"
        }, {
          id: 6,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "3"
        }, {
          id: 7,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "1"
        }, {
          id: 8,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "2"
        }, {
          id: 9,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "3"
        }, {
          id: 10,
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333,
          tag: "1"
        }
      ],
      table_title: table_title,
    }
  },
   
}
</script>


<style scoped>

</style>
