

<script>
  export default {
    props: {
      title: String
    }
}
</script>

<template>
  <div :class="$style['main']">
    <h1 :class="$style['title']">{{ title }}</h1>
    <div :class="$style['actions']">
      <slot name="search"></slot>
      <slot name="filter"></slot>
      <slot name="sort"></slot>
      <slot name="create"></slot>
      <slot name="extra"></slot>
    </div>
  </div>
</template>

<style module>

.actions{
  display: flex;
  gap: 0.5rem;
  flex-direction: row;
}

.title{
  font-size: var(--text-2xl);
  font-weight: bold;
}
.main{
  padding-top: .2rem;
  width: 100%;
  max-height: 3.2rem;
  display: flex;
  justify-content: space-between;
}
</style>

