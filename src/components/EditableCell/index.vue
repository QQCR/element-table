<template>
  <div @click="onFieldClick" class="edit-cell">
    <el-tooltip v-if="!editMode"
                :placement="toolTipPlacement"
                :open-delay="toolTipDelay"
                :content="toolTipContent">
      <div tabindex="0" 
           class="cell-content"
           @keyup.enter="onFieldClick">
        <slot name="content"></slot>
      </div>

    </el-tooltip>
    <el-input
              v-if="editMode"
              ref="input"
              v-model="model"
              @focus="onFieldClick"
              @keyup.enter.native="onInputExit"
              @blur="onInputExit"
              v-on="listeners"
              >
        <slot name="edit-component-slot"></slot>
    </el-input>
  </div>
</template>
<script>
export default {
  name: 'editable-cell',
  props: {
    value: {
      type: String,
      default: ''
    },
    toolTipContent: {
      type: String,
      default: 'Click to edit'
    },
    toolTipDelay: {
      type: Number,
      default: 500
    },
    toolTipPlacement: {
      type: String,
      default: 'top-start'
    },
    closeEvent: {
      type: String,
      default: 'blur'
    },
    row: {
      type: Object,
      default: () => {
        return null;
      }
    },
    name: {
      type: String,
      default: ''
    },
  },
  data() {
    return {
      editMode: false,
      initial: ''
    };
  },
  mounted() {
    this.initial = this.value;
  },
  computed: {
    model: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit('input', val);
      }
    },
    listeners() {
      return {
        [this.closeEvent]: this.onInputExit,
        ...this.$listeners
      };
    }
  },
  methods: {
    onFieldClick() {
      this.editMode = true;
      this.$nextTick(() => {
        let inputRef = this.$refs.input;
        if (inputRef && inputRef.focus) {
          inputRef.focus();
        }
      });

    },
    onInputExit() {
      this.editMode = false;
      this.$emit('output', this.initial, this.model, this.row, this.name);
    },
  }
};
</script>
<style>
.cell-content {
  min-height: 40px;
  padding-left: 5px;
  padding-top: 5px;
  border: 1px solid transparent;
}

</style>
