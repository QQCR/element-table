<template>
  <el-button-group>
    <el-button
      v-for="(op,index) in operations"
      :key="index"
      type="primary"
      size="mini"
      :icon="icons[op.type]"
      @click="clickOperation(op)"
    >{{op.title}}</el-button>
  </el-button-group>
</template>

<script>
export default {
  name: 'TableComponent',
  props: {
    operations: {
      type: Array
    },
    rawData: {
      type: Object
    }
  },
  data () {
    return {
      icons: {
        edit: 'el-icon-edit',
        view: 'el-icon-view'
      }
    };
  },
  created () {
  },
  methods: {
    clickOperation (operation) {
      this.$emit('handleOperation',operation,this.rawData);
    }
  }
};
</script>

