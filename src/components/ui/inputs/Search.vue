<script>
export default {
  data() {
    return {
      isFocused: false,
      search: ''
    };
  },
  methods: {
    onFocus() {
      this.isFocused = true;
    },
    onBlur() {
      this.isFocused = false;
    },
    searchChange() {
      this.$emit('SearchInputChanged', this.search);
    }
  }
}
</script>

<template>
  <div :class="[$style.text, isFocused ? $style.focused : '']">
    <img src="../../../assets/icons/search.svg" alt="search"/>
    <input
        type="text"
        v-model="search"
        @input="searchChange"
        id="search"
        :required="true"
        :value="search"
        placeholder="Поиск"
        @focus="onFocus"
        @blur="onBlur"
    />
  </div>
</template>


<style module>
input::placeholder {
  color: var(--t-c-description);
}

.text {
  display: flex;
  gap: .5rem;
  border: 1px solid;
  border-radius: var(--rounded-base);
  padding: .65rem 1rem;
  background-color: var(--white);
  border-color: var(--input-border-color);
}

.focused {
  border-color: var(--accent);
}

input:focus {
  outline: none;
}
</style>