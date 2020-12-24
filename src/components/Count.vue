<template>
  <div class="count-component">
    <div class="name">{{ value.name }}</div>
    <div class="price">￥{{ value.price }}</div>
    <div class="count">
      <button @click="action('reduce')">-</button>
      <input type="text" v-model="value.count" />
      <button @click="action('addition')">+</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    action(type) {
      if (type === "reduce") {
        // count大于0才可以减
        if (this.value.count > 0) {
          this.value.count--;
        }
      } else {
        this.value.count++;
      }
    }
  }
};
</script>

<style>
.count-component {
  display: flex;
  flex-flow: row;
  width: 100%;
  justify-content: space-between;
}
.name {
  width: 100px;
}
.price {
  width: 100px;
}
</style>
