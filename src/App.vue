<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <div class="btns-wrap">
      <el-button type="primary" size="small" icon="el-icon-sort" @click="showGeneralList"></el-button>
      <el-button type="success" size="small" icon="el-icon-top" @click="showSortedList('INCOME')"></el-button>
      <el-button type="danger" size="small" icon="el-icon-bottom" @click="showSortedList('OUTCOME')"></el-button>
    </div>
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
        id: 1,
        date: '31.04'
      },
      2: {
        type: "OUTCOME",
        value: 5000,
        comment: "Квартплата",
        id: 2,
        date: '22.05'
      },
      3: {
        type: "INCOME",
        value: 10000,
        comment: "Аванс",
        id: 3,
        date: '15.09'
      },
      4: {
        type: "OUTCOME",
        value: 2000,
        comment: "Продукты",
        id: 4,
        date: '22.05'
      }
    },
    mainList: {}
  }),

  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        item.value = Math.abs(item.value);
        if(item.type === 'INCOME') {
          return acc + item.value;
        } else if(item.type === 'OUTCOME') {
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
  margin-top: 20px;
}

body {
  background-image: linear-gradient(45deg, rgb(0, 3, 38) 0%, rgb(93, 78, 226) 100%);
}

.btns-wrap {
  max-width: 500px;
  margin: auto;
  display: flex;
}
</style>
