<template>
  <div>
    <div class="container px-4 mx-auto text-white">
      <div class="md:flex">
        <div class="md:w-2/3 md:border-r border-gray-600 xl:pt-20">
          <div class="md:flex mb-8 md:mr-4 xl:mr-10">
            <div class="flex-1">
              <h3 class="text-xl font-bold mb-4 uppercase tracking-wider">{{ leftTitle }}</h3>

              <slot name="board-members" class="mb-2"></slot>

              <a
                :href="linkDestination"
                class="text-white font-bold inline-flex items-center border-b border-white border-dashed"
              >
                {{ linkTitle }}
                <Zondicon icon="arrow-thin-right" class="fill-current w-4 ml-1" />
              </a>
            </div>
            <div class="mt-8 md:mt-0">
              <img src="~/assets/images/board19.jpg" class="w-full md:w-auto md:h-56 lg:h-64 xl:h-80 shadow-xl" />
            </div>
          </div>
        </div>

        <div class="md:ml-4 xl:ml-10 xl:pt-20 pb-8">
          <h3 class="text-xl font-bold mb-4 uppercase tracking-wider">{{ rightTitle }}</h3>
          <div class="flex items-center mb-4">
            <div class="rounded-full w-8 h-8 p-2 bg-white text-gray-700">
              <Zondicon icon="envelope" class="fill-current w-4" />
            </div>
            <div v-html="contactEmail" class="ml-3" />
          </div>
          <div class="flex items-center">
            <div class="rounded-full w-8 h-8 p-2 bg-white text-gray-700">
              <Zondicon icon="map" class="fill-current w-4" />
            </div>
            <div v-html="contactAddress" class="ml-3" />
          </div>
        </div>
      </div>
    </div>

    <hr class="border-b border-gray-600 m-0" />

    <div class="container mx-auto px-4 py-4 md:flex justify-between items-center">
      <div class="flex justify-center md:justify-start">
        <a href="https://instagram.com/outsite_delft" target="_blank">
          <div class="rounded-full w-10 h-10 p-2 bg-white text-gray-700 mr-3">
            <InstagramIcon class="fill-current w-6" />
          </div>
        </a>
        <a href="https://facebook.com/outsite" target="_blank">
          <div class="rounded-full w-10 h-10 p-2 bg-white text-gray-700 mr-3">
            <FacebookIcon class="fill-current w-6" />
          </div>
        </a>
        <a href="https://youtube.com/channel/UCtsabdS5sH7EA-DjLkBPLfQ" target="_blank">
          <div class="rounded-full w-10 h-10 p-2 bg-white text-gray-700 mr-3">
            <YouTubeIcon class="fill-current w-6" />
          </div>
        </a>
        <a href="https://github.com/dwh-outsite/outsite.nl" target="_blank">
          <div class="rounded-full w-10 h-10 p-2 bg-white text-gray-700">
            <GitHubIcon class="fill-current w-6" />
          </div>
        </a>
      </div>
      <a
        href="https://dwhdelft.nl/"
        target="_blank"
        class="text-gray-400 hover:text-white flex justify-center md:justify-end pt-4 md:pt-0"
      >
        {{ dwhDescription }}
        <DWHLogo class="h-8 ml-2 fill-current" />
      </a>
    </div>
  </div>
</template>

<script>
import Zondicon from 'vue-zondicons'
import DWHLogo from '@/assets/images/dwh_logo.svg'
import InstagramIcon from '@/assets/images/social/instagram.svg'
import FacebookIcon from '@/assets/images/social/facebook.svg'
import GitHubIcon from '@/assets/images/social/github.svg'
import YouTubeIcon from '@/assets/images/social/youtube.svg'

export default {
  components: {
    Zondicon,
    DWHLogo,
    InstagramIcon,
    FacebookIcon,
    GitHubIcon,
    YouTubeIcon
  },
  props: [
    'leftTitle',
    'rightTitle',
    'linkTitle',
    'linkDestination',
    'boardImage',
    'contactEmail',
    'contactAddress',
    'dwhDescription'
  ]
}
</script>
