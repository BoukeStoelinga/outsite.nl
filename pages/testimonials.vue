<template>
  <div>
    <header>
      <Header small="true" bg="bg-pink-100">
        <h1 class="text-4xl text-white font-normal">
          {{ $t('testimonials.title') }}
        </h1>
      </Header>
    </header>

    <section class="bg-pink-100 pt-8">
      <div class="container mx-auto px-4 pb-10 flex flex-wrap justify-center">
        <div v-for="(testimonial, index) in $t('testimonials.members')" :key="index" class="md:w-1/2 mb-8">
          <div class="md:mx-4 h-full bg-white relative rounded-lg bg-hero-falling-triangles py-6 shadow-xl">
            <div class="w-48 h-48 rounded-full overflow-hidden mx-auto">
              <img :src="requireImage(testimonial.author.name)" class="object-cover h-full" />
            </div>
            <div class="bg-white-gradient-vertical">
              <div class="text-center py-6 text-xl">
                <div v-text="testimonial.author.name" class="uppercase tracking-wide font-bold text-pink-400 mr-1" />
                <div v-text="testimonial.author.description" class="text-gray-500 italic" />
              </div>
              <div class="flex px-8 md:px-12 pb-6 leading-snug">
                <div class="absolute text-mega text-pink-100 -ml-8 -mt-20 pt-2 z-0">“</div>
                <div v-text="testimonial.text" class="text-xl z-20 pt-2" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Header from '~/components/Header'

export default {
  components: {
    Header
  },
  methods: {
    requireImage(name) {
      try {
        return require(`@/assets/images/photos/testimonials/${name.toLowerCase()}.png`)
      } catch (e) {
        return require(`@/assets/images/photos/testimonials/default.png`)
      }
    }
  }
}
</script>

<style scoped>
.page-ender::before {
  @apply bg-gray-200 absolute w-full;
  height: 40rem;
  transform: skewY(-7deg);
  content: '';
  z-index: -1;
  bottom: 0px;
}

.bg-white-gradient-vertical {
  background: rgb(255, 255, 255);
  background: linear-gradient(
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 1) 15%,
    rgba(255, 255, 255, 1) 80%,
    rgba(255, 255, 255, 0) 100%
  );
}
</style>
