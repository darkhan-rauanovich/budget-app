<template>
  <div class="total-value" :class="classObj">
    Balance: {{ total }}
  </div>
</template>

<script>
export default {
  name: 'TotalBalance',
  props: {
    total: {
      type: Number,
      default: 0,
    }
  },
  computed: {
    classObj() {
      if(this.total > 0) {
        return 'green';
      } else if(this.total < 0) {
        return 'red';
      } else {
        return 'text';
      }
    },
  }
}
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
  color: burlywood;
}
.total-value.green {
  color: green;
}

.total-value.red {
  color: red;
}

.total-value.text {
  color: black;
}
</style>