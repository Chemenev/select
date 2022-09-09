<template>
  <div
    class="drop-inner"
    :class="{
      active: isVisble === true,
    }"
    v-click-outside="hide"
  >
    <input-component
      v-model="modelValue"
      :placeholder="placeholder"
      @input="
        inputValue;
        isVisble = true;
      "
      @drop-element="addDropClass"
      @click="isVisble = true"
    />
    <div class="drop-btn" @click="isVisble = true">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        role="img"
        aria-hidden="true"
        class="v-icon__svg"
      >
        <path d="M7,10L12,15L17,10H7Z"></path>
      </svg>
    </div>
    <dropdown-component
      v-if="isVisble"
      :option="filteredArr"
      :positionClass="positionClass"
      @select-item="selectItem"
      @click="isVisble = false"
    />
  </div>
</template>
<script>
import InputComponent from '@/components/InputComponent.vue';
import DropdownComponent from '@/components/DropdownComponent.vue';

export default {
  components: { InputComponent, DropdownComponent },
  data() {
    return {
      modelValue: '',
      enterValue: '',
      positionClass: 'bottom',
      isVisble: false,
    };
  },
  props: {
    option: {
      type: Array,
      requared: true,
    },
    placeholder: {
      type: String,
    },
    defaultId: {
      type: Number,
    },
  },
  mounted() {
    if (this.option.find((i) => i.id == this.defaultId)) {
      const defaultValue = this.option.find((i) => i.id == this.defaultId);
      this.modelValue = defaultValue.name;
    }
  },
  computed: {
    filteredArr() {
      const filteredArr = this.option.filter((item) =>
        item.name.includes(this.modelValue)
      );
      return filteredArr;
    },
  },
  methods: {
    inputValue(event) {
      this.enterValue = event.target.value;
    },
    addDropClass(className) {
      this.positionClass = className;
    },
    selectItem(selectedItem) {
      this.modelValue = selectedItem.name;
      this.$emit('selected-item', selectedItem);
    },
    hide() {
      return (this.isVisble = false);
    },
  },
};
</script>
<style scoped>
.drop-inner {
  display: flex;
  align-items: center;
  position: relative;
  width: fit-content;
}
.drop-inner::before {
  content: '';
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.42);
  transition: background 0.4s;
  height: 2px;
}
.active.drop-inner::before {
  background: #000;
}
.drop-btn {
  width: 24px;
}
.drop-btn svg {
  transition: transform 0.4s;
}
.active .drop-btn svg {
  transform: rotate(180deg);
}
</style>
