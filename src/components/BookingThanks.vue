<template>
  <div class="booking-thanks">
    <v-row no-gutters>
      <v-col>
        <p>
          Thank you for selecting vKirirom Resort as your preferred resort. Your payment has been processed
          successfully.
        </p>
        <h2
          class="mb-2 font-weight-normal primary--text"
          :class="{ title: $vuetify.breakpoint.smAndDown, 'display-1': $vuetify.breakpoint.mdAndUp }"
        >
          vKirirom Pine Resort
        </h2>
        <v-row no-gutters class="mb-4">
          <v-col cols="12">
            Preah Soramarith-Kosamak National Park (Kirirom), Phnom Srouch District, Kompong Speu Province, Cambodia
          </v-col>
          <v-col cols="12">
            <a href="https://goo.gl/maps/wgVcvPnrqgYoB9bz7" class="light--text text-underline">Get Directions</a>
          </v-col>
        </v-row>
        <v-row no-gutters="" class="mb-6">
          <v-col
            ><v-icon class="text--light mr-2">phone</v-icon
            ><a class="light--text" href="tel:+(855) 78 777 284">+(855) 78 777 284</a></v-col
          >
          <v-col
            ><v-icon class="text--light mr-2">email</v-icon
            ><a class="light--text" href="mailto:info@vkirirom.com">info@vkirirom.com</a></v-col
          >
        </v-row>

        <v-row no-gutters="" class="mb-8">
          <v-col>
            <h3 class="mb-4 title font-weight-bold">Need Transportation?</h3>
            <p class="mb-8">
              vKirirom Pine Resort offers a easy shuttle service for visitors between Kirirom and Phnom Penh. Click to
              reserve your shuttle now.
            </p>
            <v-btn
              href="http://shuttlebus.vkirirom.com/login"
              large
              color="primary"
              dark
              class="text-transform-none font-weight-bold dark--text"
            >
              <span class="px-4">Sign Up Now</span>
              <v-icon>keyboard_arrow_right</v-icon>
            </v-btn>
          </v-col>
        </v-row>

        <h3 class="mb-4 title font-weight-bold">Room Description</h3>
        <resort-description :resort="resort"></resort-description>

        <v-btn class="mt-6 text-transform-none" outlined="" dark large to="/"
          ><span class="mx-4">Return to Home</span><v-spacer></v-spacer><v-icon>keyboard_arrow_right</v-icon></v-btn
        >
      </v-col>
    </v-row>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import store from '../store';
// import ResortRules from '@/components/ResortRules.vue'
const ResortDescription = () => import('@/components/ResortDescription.vue');
import { Resort } from '../types';
import marked from 'marked';

// https://marked.js.org/
marked.setOptions({
  renderer: new marked.Renderer(),
  pedantic: false,
  gfm: true,
  breaks: false,
  sanitize: false,
  smartLists: true,
  smartypants: false,
  xhtml: false
});
export default Vue.extend({
  name: 'booking-thanks',
  components: { ResortDescription },
  computed: {
    resort() {
      return (this as any).$store.getters['booking/bookingInfo'].resort;
    }
  },
  methods: {
    marked(content) {
      if (!content) {
        return '';
      }
      return marked(content);
    }
  }
});
</script>

<style lang="scss">
@import '@/styles/utility.scss';
</style>

<style lang="scss" scoped>
.v-application .theme--light.v-icon {
  color: map-get($grey, 'lighten-1');
}
.booking-thanks::v-deep h3 {
  margin-bottom: rem(16px);
}
</style>
