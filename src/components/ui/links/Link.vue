<script>

import {computed, useCssModule } from "vue";

export default {
  props: {
    isActive: {
      type: Boolean,
      default: false
    },
    image: {
      type: String,
      default: null,
    },
    href: {
      type: String,
      default: null,
    },
    text: {
      type: String,
      default: null,
    }
  },

  setup(props, ctx) {
    const style = useCssModule()

    const activeLink = computed(() => {
      if (props.isActive) {
        return [style.link, style.isActive];
      }else{
        return [style.base, style.link]
      }
    })

    const imageColor = computed(() => {
      if (props.isActive) return [style.link, style.isActive];

      else return [style.base, style.link]
    })

    return {
      activeLink
    }
  }
}

</script>

<template>
  <a :href="href" :class="activeLink" >
    <img :src="image" :alt="text" class="image" v-show="image" />
    <div >
      {{text}}
    </div>
  </a>
</template>

<style module>

.isActive {
  background-color: var(--accent);
  color: var(--white);
}
.isActive:hover{
  opacity: 0.8;
}

.base{
  color: var(--black);
  background-color: var(--white);
}
.base:hover{
  background-color: var(--foregroound);
  color: var(--black);
}


.link{
  min-height: 2.5rem; /* h-10 */
  padding: 0.5rem 1rem; /* py-2 px-4 */
  display: inline-flex;
  width: 100%;
  gap: 0.5rem;
  align-items: center;
  border-radius: var(--rounded-base); /* rounded-md */
  font-weight: 500; /* font-medium */
  transition: all 0.2s ease-in-out ;
  outline: none;
  cursor: pointer;
  user-select: none;;
}

</style>

