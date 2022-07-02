<template>
  <div class="budget-list-wrap">
    <div class="buttons">
      <el-button type="success" @click="sortIn">Income</el-button>
      <el-button type="danger" @click="sortOut">Outcome</el-button>
      <el-button type="primary" @click="sortAll">All</el-button>
    </div>
    <el-card :header="header">
      <template v-if="isEmpty">
        <!-- {{ sortList }} -->
        <BudgetListItem v-for="(item, prop) in sortList" :key="prop" :item="item" @deleteItem="deleteItem"/>
      </template>
      <el-alert v-else type="info" :title="emptyTitle" :closable="false"></el-alert>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from './BudgetListItem.vue'

export default {
  name: 'BudgetList',
  components: {
    BudgetListItem
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    }
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty list',
    sortName: 'ALL',
  }),
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
    sortIn() {
      this.sortName = 'INCOME'
    },
    sortOut() {
      this.sortName = 'OUTCOME'
    },
    sortAll() {
      this.sortName = 'ALL'
    }
  },
  computed: {
    isEmpty() {
      return Boolean(Object.keys(this.list).length);
    },
    sortList() {
      if(this.sortName == 'INCOME') {
        const obj = Object.values(this.list).reduce((acc,item) => {
          if(item.type == 'INCOME') {
            acc[item.id] = item;
          }
          return acc;
        },{})
        return obj;
      } else if(this.sortName == 'OUTCOME') {
        return Object.values(this.list).reduce((acc,item) => {
          if(item.type == 'OUTCOME') {
            acc[item.id] = item;
          }
          return acc;
        },{})
      } else {
        return this.list;
      }
    }
  }
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.buttons {
  margin: 0 0 20px 0;
}
</style>