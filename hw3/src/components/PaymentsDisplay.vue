<template>
<div>
  <div :class="$style.wrapper">
      <table :class="$style.list">
        <thead>
          <tr>
            <th>#</th>
            <th>Date</th>
            <th>Category</th>
            <th>Value</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.date }}</td>
            <td>{{ item.category }}</td>
            <td>{{ item.value }}</td>
          </tr>
        </tbody>
      </table>
    </div>
</div>
</template>

<script>
export default {
  name: 'PaymentsDisplay',
  props: {
    items: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" module>
.list {
  width: 100%;
  font-size: 1.25rem;
  border-collapse: collapse;
  td {
    padding: 0.5em;
    text-align: center;
  }
}
</style>
