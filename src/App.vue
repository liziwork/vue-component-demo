<template>
  <div id="app">
    <Count
      v-for="source in sources"
      :key="source.number"
      v-bind:value="source"
    />
    <div class="sources">
      <div v-for="item in sources" :key="item.name">
        {{ item.name }}:{{ item.count }}
      </div>
    </div>
    <div class="numbers">
      <div v-for="item in numberCountItem" :key="item.name">
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
import Count from "./components/Count.vue";

export default {
  name: "App",
  components: {
    Count
  },
  data() {
    return {
      sources: [
        {
          number: "N034",
          name: "男士",
          price: 15,
          count: 0
        },
        {
          number: "V034",
          name: "女士",
          price: 15,
          count: 0
        },
        {
          number: "E034",
          name: "儿童",
          price: 7,
          count: 0
        }
      ]
    };
  },
  computed: {
    numberCountItem() {
      const numbers = this.sources.map(v => {
        let list = [];
        let item = v.number;
        for (let i = 0; i <= v.count; i++) {
          item = this.format(item);
          list.push(item);
        }
        return list;
      });
      return [].concat.apply([], numbers);
    }
  },
  methods: {
    format(item) {
      const count = item.match(/(\d+)([^\d]*)$/i)[1];
      return item.replace(
        /(\d+)([^\d]*)$/i,
        this.PrefixInteger(Number(count) + 1, count.length) + "$2"
      );
    },
    PrefixInteger(num, n) {
      return (Array(n).join(0) + num).slice(-n);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 500px;
  display: flex;
  flex-flow: column;
  align-items: center;
}
.sources {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 10px 0;
}
.numbers > div {
  float: left;
  padding: 4px 0;
}
.numbers > div::after {
  content: "、";
}
.numbers > div:last-child::after {
  display: none;
}
</style>
