<template>
  <div class="list-item">
    <span class="budget-date">{{ date }}</span>
    <span class="budget-comment">{{ comment }}</span>
    <span class="budget-value" :class="valueClass"> {{ value }}</span>
    <el-button type="danger" size="mini" @click="deleteItemTemplate(id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  data: () => ({
    valueClass: ""
  }),

  props: {
    comment: {
      type: String,
      default: "No comment"
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
    },
    date: {
      type: String
    }
  },

  methods: {
    deleteItemTemplate(id) {
      if (confirm("Вы подтверждаете удаление???")) {
        this.$emit("deleteItemTemplate", id);
      }
    },

    setItemStyle() {
      switch (this.comeType) {
        case "INCOME":
          this.valueClass = "el-icon-top color-green";
          break;

        case "OUTCOME":
          this.valueClass = "el-icon-bottom color-red";
          break;
      }
    }
  },

  mounted() {
    this.setItemStyle();
  }
};
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

.budget-comment {
  margin-left: 10px;
  font-weight: bold;
}

.budget-date {
  font-size: 14px;
  border-radius: 5px;
  border: 1px rgb(93, 78, 226) solid;
  padding: 2px 3px;
}
</style>
