<script>

import {computed, useCssModule } from "vue";

export default {
  props: {
    isActive: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: "default"
    },
    image: {
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

    const buttonIsActive = computed(() => {
      if (props.isActive) {
        return [style.button, style.isActive];
      }else{
        return style.button
      }
    })

    const typeButton= computed(() => {
      switch (props.type) {
        case "outlet":
          return [style.button, style.outlet];
        case "foreground":
          return [style.button, style.foreground];
        default:
          return [style.button, style.default];
      }
    })

    return {
      typeButton,
      buttonIsActive
    }
  }
}

</script>

<template>
  <button :class="typeButton, buttonIsActive">
    <img :src="image"
         v-show="image"
         alt="button-image" class="image" />
    <div class="text" v-show="text">
      {{text}}
    </div>
  </button>
</template>

<style module>

.image{
  width: 24px;
  height: 24px;
}

.button {
  min-height: 2.5rem; /* h-10 */
  padding: 0.5rem 1rem; /* py-2 px-4 */
  display: inline-flex;
  gap: 0.5rem;
  align-items: center;
  color: var(--white);
  border-radius: var(--rounded-base); /* rounded-md */
  font-weight: 500; /* font-medium */
  transition: all 0.2s ease-in-out ;
  outline: none;
  cursor: pointer;
  user-select: none;
}
.button:hover {
  border: 1px solid rgba(55, 97, 243, 1);
}
.text{
  display: block;
  width: fit-content;
}

.default{
  background-color: rgba(55, 97, 243, 1);
}

.button:disabled{
  opacity: 0.5;
  cursor: not-allowed ;
  pointer-events: visibleFill;
}

/*VARIANTS*/
.foreground {
  border: 1px solid transparent;
  background-color: var(--foregroound);
  color: var(--black);
}
.foreground:hover{
  border-color: var(--foregroound);
  background-color: var(--white);
}
.foreground:focus-visible {
  outline: 2px solid var(--accent); /* custom ring color */
  outline-offset: 2px;
}



.ghost:hover{
  color: var(--accent); /* text-accent-foreground */
  background: var(--b-ghostHover-color);
}



.default:focus-visible {
  outline: 2px solid var(--t-c-description); /* custom ring color */
  outline-offset: 2px;
}
.default:hover{
  background: var(--foregroound); /* text-accent-foreground */
  color: var(--black);
}

.outlet{
  background: var(--white);
  color: var(--black);
  border: 1px solid var(--t-c-description);
}
.outlet:disabled{
  background-color: var(--t-c-description);
  color: white;
  border: none;
}



</style>
