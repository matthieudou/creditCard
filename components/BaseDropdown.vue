<template>
  <div class="relative">
    <span class="inline-block w-full rounded-md shadow-sm">
      <button
        type="button"
        aria-haspopup="listbox"
        aria-expanded="true"
        aria-labelledby="listbox-label"
        class="cursor-default relative w-full rounded-md border border-gray-300 bg-white pl-3 pr-10 py-2 text-left focus:outline-none focus:shadow-outline-blue focus:border-blue-300 transition ease-in-out duration-150 sm:text-sm sm:leading-5"
        @click="isOpen = !isOpen"
      >
        <div class="flex items-center space-x-3">
          <img
            :src="value.img"
            alt
            class="flex-shrink-0 h-6 w-6 object-contain"
          >
          <span class="block truncate">{{ value.name }}</span>
        </div>
        <span class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
          <svg class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="none" stroke="currentColor">
            <path
              d="M7 7l3-3 3 3m0 6l-3 3-3-3"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </span>
      </button>
    </span>

    <transition @enter="enter" @leave="leave">
      <div v-if="isOpen" class="absolute mt-1 w-full rounded-md bg-white shadow-lg">
        <ul
          tabindex="-1"
          role="listbox"
          aria-labelledby="listbox-label"
          aria-activedescendant="listbox-item-3"
          class="max-h-56 rounded-md py-1 text-base leading-6 shadow-xs overflow-auto focus:outline-none sm:text-sm sm:leading-5"
        >
          <li
            v-for="option in filteredOptions"
            id="listbox-item-0"
            ref="attribute"
            :key="option.key"
            role="option"
            class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-gray-100 transition-color duration-100 ease-in-out"
            @click="selectOption(option)"
          >
            <div class="flex items-center space-x-3">
              <img
                :src="option.img"
                alt
                class="flex-shrink-0 h-6 w-6 object-contain"
              >
              <span class="font-normal block truncate">{{ option.name }}</span>
            </div>
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
import { gsap } from 'gsap'

export default {
  props: {
    options: {
      type: Array,
      default: () => []
    },

    value: {
      type: [String, Object],
      default: ''
    },

    trackBy: {
      type: String,
      default: null
    }
  },

  data () {
    return {
      isOpen: false
    }
  },

  computed: {
    filteredOptions () {
      return this.options.filter((item, x) => x !== this.selectedIndex)
    },

    selectedIndex () {
      return this.options.findIndex(x => x.key === this.value.key)
    }
  },

  methods: {
    selectOption (value) {
      this.$emit('input', value)
    },

    enter (el, done) {
      gsap
        .timeline({ onComplete: done, defaults: { ease: 'back.inOut(3)' } })
        .from(el, {
          autoAlpha: 0,
          translateY: 30,
          duration: 0.3
        })
        .from(this.$refs.attribute, {
          autoAlpha: 0,
          translateX: -10,
          duration: 0.1,
          stagger: 0.05
        }, '-=0.2')
        .set(el, { clearProps: 'all' })
        .set(this.$refs.attribute, { clearProps: 'all' })
    },

    leave (el, done) {
      gsap
        .timeline({ onComplete: done, defaults: { ease: 'back.inOut(3)' } })
        .to(this.$refs.attribute, {
          autoAlpha: 0,
          translateX: -10,
          duration: 0.1,
          stagger: -0.05
        })
        .to(el, {
          autoAlpha: 0,
          translateY: 30,
          duration: 0.3
        }, '-=0.2')
        .set(this.$refs.attribute, { clearProps: 'all' })
        .set(el, { clearProps: 'all' })
    }
  }
}
</script>
