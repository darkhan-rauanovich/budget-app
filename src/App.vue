<template>
  <div class="main">
    <FormEl @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>


<script>

import BudgetList from './components/BudgetList.vue'
import TotalBalance from './components/TotalBalance.vue'
import FormEl from './components/Form.vue'

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    FormEl,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      },
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        if(item.type === 'INCOME') {
          return acc + item.value;
        }else {
          return acc - item.value;
        }
      }, 0)
    },
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObject = {
        ...data,
        id: String(Math.random())
      };

      this.$set(this.list, newObject.id, newObject)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
