<template>
  <div>
    <table-page
      :list="list"
      :table_title="table_title"
      :operates="operates"
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
      <template v-slot:operates="scope">
        <table-operation 
          :operations="operations"
          :rawData="scope.scope.row"
          @handleOperation="handleOperation"
        ></table-operation>
      </template>
    </table-page>
    <el-dialog title="编辑" :visible.sync="editDialog">
      <el-form :model="editInfo" label-position="left">
        <el-form-item label="日期" :label-width="formLabelWidth">
          <el-input v-model="editInfo.date"></el-input>
        </el-form-item>
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="editInfo.name"></el-input>
        </el-form-item>
        <el-form-item label="省份" :label-width="formLabelWidth">
          <el-input v-model="editInfo.province"></el-input>
        </el-form-item>
        <el-form-item label="市区" :label-width="formLabelWidth">
          <el-input v-model="editInfo.city"></el-input>
        </el-form-item>
        <el-form-item label="地址" :label-width="formLabelWidth">
          <el-input v-model="editInfo.address"></el-input>
        </el-form-item>
        <el-form-item label="状态" :label-width="formLabelWidth">
          <el-select v-model="editInfo.tag" placeholder="请选择tag" style="display: block;">
            <el-option label="tag1" value="1"></el-option>
            <el-option label="tag2" value="2"></el-option>
            <el-option label="tag3" value="3"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="closeDialog">取 消</el-button>
        <el-button type="primary" @click="saveDialog">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import TablePage from '@/components/TablePage'
import TableOperation from '@/components/TableOperation'

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

const operates = {
  operate: true,
  label: '操作',
  minwidth: '120px',
  titleAlign: 'center',
  columnAlign: 'center',
};

const operations = [
  {
    type: 'edit',
    title: '编辑'
  },
  {
    type: 'view',
    title: '查看'
  }
];

export default {
  components: {
    TablePage,
    TableOperation
  },
  data() {
    return {
      list: [{
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
      total: 10,
      operates: operates,
      operations:operations,
      editDialog: false,
      editInfo: {
        id: 0,
        date: '',
        name: '',
        province: '',
        city: '',
        address: '',
        tag: 0
      },
      formLabelWidth: '100px'
    }
  },
  methods: {
    handleOperation(op,row) {
      console.log(op,row)
      if (op.type == 'edit') {
        this.editDialog = true
        this.editInfo.id = row.id
        this.editInfo.date = row.date
        this.editInfo.name = row.name
        this.editInfo.province = row.province
        this.editInfo.city = row.city
        this.editInfo.address = row.address
        this.editInfo.tag = row.tag
      }
      else if (op.type == 'view') {
        alert ('view!!!')
      }
    },
    closeDialog() {
      this.editDialog = false
    },
    saveDialog() {
      this.editDialog = false
      let info = this.editInfo
      this.list.forEach(item => {
        if(item.id === info.id) {
          for ( var key in info) {
            item[key] = info[key];
          }
        }
      })
    },
    editChange(oldV, newV, row, name) {
      this.list.forEach(item => {
        if(item.id === row.id) {
          item[name] = newV
        }
      })
    }
  }
}
</script>


<style scoped>

</style>
