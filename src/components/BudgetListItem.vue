<template>
  <div class="list-item">
    <span>{{ comment }}</span>
    <span class="budget-value" :class="valueClass"> {{ value }}</span>
    <el-button type="danger" size="mini" @click="deleteItemTemplate(id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  data: () => ({
    valueClass: '',
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
          this.valueClass = 'el-icon-top color-green';
          break;

        case 'OUTCOME':
          this.valueClass = 'el-icon-bottom color-red';
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

.color-green {
  color: green;
}

.color-red {
  color: red;
}
</style>