<template>
  <div class="list-item " :class="icon">
    <span class="budget-comment">{{ comment }}</span>
    <span class="budget-value" :style="{'color': valueColor}">{{ value }}</span>
    <el-button type="danger" size="mini" @click="deleteItemTemplate(id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  data: () => ({
    icon: '',
    valueColor: ''
  }),
  props: {
    comment: {
      type: String,
      default: 'No comment'
    },
    value: {
      type: Number,
      default: 0
    },
    id: {
      type: Number
    },
    comeType: {
      type: String
    }
  },
  methods: {
    deleteItemTemplate(id) {
      if(confirm('Вы подтверждаете удаление???')) {
        this.$emit("deleteItemTemplate", id);
      }
    },
    setItemStyle() {
      switch (this.comeType) {
        case 'INCOME':
          this.icon = 'el-icon-top';
          this.valueColor = 'green';
          break;

        case 'OUTCOME':
          this.icon = 'el-icon-bottom';
          this.valueColor = 'red';
          break;
      }
    },
  },
  mounted() {
    this.setItemStyle();
  }
}
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}

.budget-comment {
  margin-left: 10px;
}
</style>