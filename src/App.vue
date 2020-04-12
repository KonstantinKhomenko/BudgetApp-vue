<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <el-button type="primary" size="mini" plain @click="showGeneralList">Show all</el-button>
    <el-button type="success" size="mini" plain @click="showSortedList('INCOME')">Only Income</el-button>
    <el-button type="danger" size="mini" plain @click="showSortedList('OUTCOME')">Only Outcome</el-button>
    <BudgetList :list="mainList" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";

export default {
  name: "app",
  components: {
    BudgetList,
    TotalBalance,
    Form
  },

  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 25000,
        comment: "Зарплата",
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: 5000,
        comment: "Квартплата",
        id: 2
      },
      3: {
        type: "INCOME",
        value: 10000,
        comment: "Аванс",
        id: 3
      },
      4: {
        type: "OUTCOME",
        value: 2000,
        comment: "Продукты",
        id: 4
      }
    },
    mainList: {}
  }),

  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        if(item.type === 'INCOME') {
          return acc + item.value;
        } else if(item.type === 'OUTCOME') {
          if(item.value < 0) {
            item.value = Math.abs(item.value);
          }
          return acc - item.value;
        }
      }, 0);
    }
  },

  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },

    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    },

    showGeneralList() {
      this.templateObj(this.list);
    },

    templateObj(obj) {
      this.mainList = {
        ...obj
      };
    },

    showSortedList(itemType) {
      const sortArr = Object.values(this.list).filter(item => item.type === itemType);
      const sortObj = sortArr.reduce((acc, item) => {
        acc[item.id] = item;
        return acc;
      }, {});

      this.templateObj(sortObj);
    }
  },

  mounted() {
    this.showGeneralList();
  },

  watch: {
    list: 'showGeneralList'
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

body {
  background-image: linear-gradient(45deg, rgb(0, 3, 38) 0%, rgb(93, 78, 226) 100%);
}
</style>
