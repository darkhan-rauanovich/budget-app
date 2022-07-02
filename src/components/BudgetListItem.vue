<template>
  <div class="list-item">
    <span class="budget-comment">{{ item.comment }}</span>
    <span class="budget-value">{{ item.value }}</span>
    <i class="icon-item" :class="classIcon"></i>
    <el-button type="danger" @click="deleteItem(item.id)" size="mini">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  props: {
    item: {
      type: Object,
      default: () => ({})
    }
  },
  methods: {
    deleteItem(id) {
      const confirmDelete = confirm('Are you sure you want to delete');
      if(confirmDelete) {
        this.$emit('deleteItem', id);
      }
    }
  },
  computed: {
    classIcon() {
      if(this.item.type === 'INCOME') {
        return 'el-icon-top';
      } else {
        return 'el-icon-bottom';
      }
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
  margin-right: 20px;
  margin-left: auto;
}

.icon-item {
  margin-right: 20px;
  margin-left: 20px;
  font-weight: 800;
}

.icon-item.el-icon-top {
  color: green;
}

.icon-item.el-icon-bottom {
  color: red;
}

</style>