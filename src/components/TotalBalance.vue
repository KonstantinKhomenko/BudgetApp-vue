<template>
  <div class="total-value" :style="totalColor">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: 'TotalBalance',
  data: () => ({
    balanceColor: ''
  }),
  props: {
    total: {
      type: Number,
      default: 0,
    }
  },
  watch: {
    total: 'changeTotalColor'
  },
  computed: {
    totalColor() {
      return {
        'color': this.balanceColor,
        'border': `3px ${this.balanceColor} solid`
      }
    }
  },
  methods: {
    changeTotalColor(value) {
      if(value === 0) {
        this.balanceColor = 'black';
      } else if(value > 0) {
        this.balanceColor = 'green';
      } else {
        this.balanceColor = 'red';
      }
    }
  },
  mounted() {
    this.changeTotalColor(this.total);
  }
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  padding: 20px;
  text-align: center;
  margin: 10px 0;
  background-color: #ffffff;
  border-radius: 10px;
  display: inline-block;
  width: 300px;
}
</style>