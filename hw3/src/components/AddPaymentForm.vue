<template>
  <div>
   <div :class="$style.addpayform">
      <input type="date" placeholder="Date" v-model="date" :class="$style.input">
      <input type="text" :placeholder="categoryPlaceholder" v-model="category" :class="$style.input">
      <input type="number" :placeholder="valuePlaceholder" v-model="value" :class="$style.input">
      <button @click="addPayment" :class="$style.addbutton">Add  +</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddPaymentForm',
  components: {},
  props: {},
  data () {
    return {
      value: '',
      category: '',
      date: '',
      categoryPlaceholder: 'Category',
      valuePlaceholder: 'Value'
    }
  },
  methods: {
    addPayment () {
      const { date, category, value } = this
      const data = { date: date || this.currentDate, category, value: +value }
      if (data.category !== '' && data.value !== 0) {
        this.$emit('add-payment', data)
      }
      this.categoryPlaceholder = 'Enter category !!!'
      this.valuePlaceholder = 'Enter value !!!'
    }
  },
  computed: {
    currentDate () {
      const d = new Date()
      const date = d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate()
      return date
    }
  }
}
</script>

<style lang="scss" module>

.addpayform {
  display: flex;
  flex-direction: column;
  gap: 20px;
  clear: both;
}
.input {
  padding: 5px 10px;
  font-size: 20px;
  color: #a2b1a3;
}
.addbutton{
  color: #fff;
  font-size: 18px;
  background-color:#2aa694;
  padding: 5px 15px;
  margin-bottom: 30px;
  border: 0;
  cursor: pointer;
  &:hover {
     color:#2aa694;
     background-color:#ffffff;
  }
}
</style>
