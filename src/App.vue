<template>
  <div class="container">
    <form novalidate>
      <select-component
        :option="arr"
        :placeholder="placeholder"
        :defaultId="1"
        @selected-item="select"
      />
    </form>
  </div>
</template>

<script>
import SelectComponent from './components/SelectComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      arr: [
        { id: '1', name: 'Апельсин' },
        { id: '2', name: 'Тыква' },
        { id: '3', name: 'Картофель' },
        { id: '4', name: 'Ананас' },
      ],
      placeholder: 'Начните ввод',
    };
  },
  components: {
    SelectComponent,
  },
  methods: {
    select(selectedItem) {
      console.log(selectedItem);
    },
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  width: 88%;
}
</style>
