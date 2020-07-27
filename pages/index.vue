<template>
  <main class="bg-gray-200 min-h-screen text-gray-900">
    <div class="max-w-screen-lg mx-auto px-8 md:px-10 lg:px-12 pt-32">
      <h1 class="text-3xl font-medium">
        Credit card animation
      </h1>
      <p class="mt-4 mb-8 text-gray-700">
        Little credit card animation with GSAP, based on the bank name
      </p>
      <div class="rounded-lg bg-white shadow-sm p-12 grid grid-cols-2 gap-12">
        <div class="max-w-sm">
          <label class="block text-sm leading-5 font-medium text-gray-700">
            <div class="mb-1">Bank account</div>
            <input v-model="account" v-mask="'BE## #### #### ####'" class="form-input w-full">
          </label>

          <label class="mt-8 block text-sm leading-5 font-medium text-gray-700">
            <div class="mb-1">Bank name</div>
            <base-dropdown v-model="selectedBank" :options="bankNames" />
          </label>
        </div>

        <div class="flex justify-end">
          <credit-card class="h-56 w-auto" :bank="selectedBank" track-by="key" :account="account" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { mask } from 'vue-the-mask'

export default {
  directives: { mask },

  data () {
    return {
      bankNames: [
        {
          key: 'bnp',
          name: 'BNP Paribas Fortis',
          img: require('~/assets/images/banks/bnp.png'),
          color: 'rgba(8, 137, 101, 1.00)'
        },
        {
          key: 'belfius',
          name: 'Belfius',
          img: require('~/assets/images/banks/belfius.png'),
          color: 'rgba(195, 0, 70, 1.00)'
        },
        {
          key: 'crelan',
          name: 'Crelan',
          img: require('~/assets/images/banks/crelan.png'),
          color: 'rgba(42, 116, 85, 1.00)'
        },
        {
          key: 'bpost',
          name: 'BPOST banque',
          img: require('~/assets/images/banks/bpost.png'),
          color: 'rgba(181, 6, 6, 1.00)'
        },
        {
          key: 'axa',
          name: 'Axa',
          img: require('~/assets/images/banks/axa.png'),
          color: 'rgba(5, 0, 149, 1.00)'
        },
        {
          key: 'ing',
          name: 'ING',
          img: require('~/assets/images/banks/ing.png'),
          color: 'rgba(255, 102, 10, 1.00)'
        }
      ],
      selectedBank: {
        key: 'ing',
        name: 'ING',
        img: require('~/assets/images/banks/ing.png'),
        color: 'rgba(255, 102, 10, 1.00)'
      },
      account: 'BE70 3630 7714 2625'
    }
  }
}
</script>
