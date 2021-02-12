<template>
  <div class="table">
    <div class="table-header">
      <div class="table-column">Stock</div>
      <div class="table-column">Current</div>
      <div class="table-column">Change</div>
    </div>
    <div class="table-body">
      <div class="table-row" v-for="(item, index) in sortedData" :key="index">
        <div class="table-row__item">{{ item.name }}</div>
        <div class="table-row__item">{{ item.current }}</div>
        <div class="table-row__item" :class="item.change >= 0 ? 'success' : 'danger'">{{ item.change }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    sortedData() {
      return this.data.stocks
          .map((item, index) => {
            const name = item
            const current = this.data.current[index].toFixed(2)
            const change = (this.data.current[index] - this.data.start[index]).toFixed(2)
            return {name, current: +current, change: +change}
          })
          .sort((a, b) => {
            if (a.name < b.name) return -1
            if (a.name > b.name) return 1
            return 0
          })
    }
  }
}
</script>

<style lang="scss">
.table {
  max-width: 280px;
  width: 100%;
  margin: 0 auto;
  text-align: start;
  border: 1px solid #EEEEEE;

  &-header {
    display: flex;
    font-size: 14px;
    font-weight: 600;
    background-color: #F5F5F5;
    border-bottom: 1px solid #EEEEEE;
  }

  &-row {
    display: flex;
    border-bottom: 1px solid #EEEEEE;

    &:last-child {
      border: none;
    }

    &__item {
      font-size: 14px;

      &.success {
        color: #65A227;
      }

      &.danger {
        color: #b73939;
      }
    }
  }

  &-column, &-row__item {
    max-width: calc(100% / 3);
    width: 100%;
    padding: 5px 13px;

    &:nth-child(2) {
      text-align: center;
    }

    &:nth-child(3) {
      text-align: end;
    }
  }
}
</style>
