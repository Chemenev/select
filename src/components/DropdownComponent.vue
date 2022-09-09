<template>
  <div class="dropdown-list" :class="positionClass">
    <div
      class="dropdown-list__item"
      v-for="item in option"
      :key="item.id"
      @click="selectItem(item)"
    >
      {{ item.name }}
    </div>
    <div v-if="option == ''" class="list__item">не найдено</div>
  </div>
</template>

<script>
export default {
  props: {
    option: {
      type: Array,
    },
    positionClass: {
      type: String,
    },
  },
  methods: {
    selectItem(item) {
      this.$emit('select-item', item);
    },
  },
};
</script>
<style scoped>
.dropdown-list {
  position: absolute;
  width: 100%;
  font-size: 16px;
  font-family: sans-serif;
  background: #fff;
  box-shadow: 0 4px 6px 0 rgb(32 33 36 / 28%);
}
.dropdown-list__item {
  cursor: pointer;
  padding: 12px 18px;
}
.dropdown-list__item:hover {
  background: #fafafa;
}
.top {
  bottom: 100%;
}
.bottom {
  top: 100%;
}
</style>
