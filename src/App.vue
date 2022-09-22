<template>
  <div class="container">
    <form novalidate>
      <select-component
        :options="products"
        placeholder="Начните ввод"
        :defaultId="1"
        @selected="select"
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
      products: [
        { id: '1', name: 'Апельсин' },
        { id: '2', name: 'Тыква' },
        { id: '3', name: 'Картофель' },
        { id: '4', name: 'Ананас' },
      ],
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
