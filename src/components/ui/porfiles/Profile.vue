<script>

// import {computed, useCssModule } from "vue";

import {useCssModule} from "vue";

export default {
  props: {
    status: {
      type: String,
      default: "Пользователь"
    },
    name: {
      type: String,
      default: null,
    },
  },


}

</script>

<template>
  <a href="https://github.com/FOLLOO" :class="$style['main']">
    <div :class="$style['info']">
      <h5>{{name}}</h5>
      <p>{{status}}</p>
    </div>
    <div :class="$style['profile']">
      {{name[0] + name[name.indexOf(' ') + 1]}}
    </div>
  </a>
</template>

<style module>
.info{
 width: 100%;
}

.info h5{
  font-weight: bold;
}

.info p{
  font-size: var(--text-sm);
  color: var(--t-c-description);
}

.profile{
  width: 100%;
  border-radius: 100%;
  max-width: 4rem;
  height: 4rem;
  color: var(--white);
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  background: var(--accent);
}

.main{
  cursor: pointer;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: .75rem;
  gap: .75rem;
  /* sc_base-6 */
  background: var(--white);
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.12);
  border-radius: var(--rounded-base);
}
</style>

