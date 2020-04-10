<template>
  <div class="list-item" >
    <span class="budget-comment">{{ comment }}</span>
    <span class="budget-value">{{ value }}</span>
    <el-button type="danger" size="mini" @click="deleteItemTemplate(id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
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
    }
  },
  methods: {
    deleteItemTemplate(id) {
      this.$emit("deleteItemTemplate", id);
    }
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
</style>