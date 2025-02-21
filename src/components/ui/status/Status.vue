<script>

import {computed, useCssModule } from "vue";

export default {
  props: {
    type: {
      type: String,
      default: "default"
    },
  },

  setup(props, ctx) {
    const style = useCssModule()

    const statusStyle = computed(() => {
      switch (props.type){
        case "planned":
          return [style.status, style.planned]
        case "completed":
          return [style.status, style.completed]
        case "canceled":
          return [style.status, style.canceled]
        default: return "default"
      }
    })

    const statusText = computed(() => {
      switch (props.type){
        case "planned":
          return "Запланировано"
        case "completed":
          return "Завершено"
        case "canceled":
          return "Отменено"
        default: return "default"
      }
    })

    return {
      statusStyle, statusText
    }
  }
}

</script>

<template>
  <div :class="statusStyle">
    {{statusText}}
  </div>
</template>


<style module>

.canceled{
  background-color: var(--light-red);
}

.completed{
  background-color: var(--light-green);
}

.planned{
  background-color: var(--light-blue);
}

.status{
  font-weight: 500;
  justify-content: center;
  display: flex;
  align-items: flex-start;
  padding: .25rem .75rem;
  border-radius: var(--rounded-base);
}





</style>
