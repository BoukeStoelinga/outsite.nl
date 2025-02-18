<template>
  <div>
    <header>
      <Header small="true">
        <h1 class="text-4xl text-white font-normal">
          {{ $t('ways_to_join.bar_buddy.title') }}
        </h1>
      </Header>
    </header>

    <section class="container mx-auto pb-4 text-xl md:text-2xl leading-normal text-gray-800">
      <div class="md:w-2/3 mx-4 md:mx-auto">
        <p v-html="$t('ways_to_join.bar_buddy.description')" class="mt-8 mb-4 md:mt-0 md:mb-12" />
      </div>
    </section>

    <section class="bg-pink-200">
      <div class="container px-4 mx-auto pt-8 pb-12">
        <div class="text-center">
          <h1 v-html="$t('ways_to_join.bar_buddy.barbuddies_title')" class="text-white font-medium text-5xl" />
        </div>
        <div class="md:flex flex-wrap -mx-2 mt-2">
          <div v-for="buddy in barbuddies" :key="buddy.name" class="md:w-1/2 p-2">
            <div class="bg-white rounded shadow p-6 md:p-8">
              <div class="flex justify-between items-center mb-4">
                <div class="flex items-center">
                  <div class="rounded-full w-12 h-12 p-3 bg-pink-400 text-white">
                    <Zondicon icon="user" class="fill-current" />
                  </div>
                  <h2 class="text-2xl font-bold ml-3 text-pink-400 uppercase tracking-wider">
                    {{ buddy.name }}
                  </h2>
                </div>
                <button @click="meetWith(buddy)" class="button-pink flex items-center hidden md:flex">
                  {{ $t('ways_to_join.bar_buddy.meet_up_with') }} {{ buddy.name }}
                  <Zondicon icon="arrow-thin-right" class="ml-2 w-4 fill-current" />
                </button>
              </div>
              <p :class="['text-lg relative', buddy.readMore ? 'pb-8' : 'clamp-lines']">
                <span class="absolute bottom-0 right-0 flex">
                  <span class="w-32 block white-gradient" />
                  <a @click="readMore(buddy)" class="text-pink-400 bg-white cursor-pointer">
                    {{ $t('ways_to_join.bar_buddy.' + (buddy.readMore ? 'read_less' : 'read_more')) }}
                  </a>
                </span>
                {{ buddy.bio }}
              </p>
              <button @click="meetWith(buddy)" class="button-pink flex items-center mt-4 flex md:hidden">
                {{ $t('ways_to_join.bar_buddy.meet_up_with') }} {{ buddy.name }}
                <Zondicon icon="arrow-thin-right" class="ml-2 w-4 fill-current" />
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="form" class="bg-gray-200 pt-12 pb-12">
      <div class="mx-auto container">
        <h2 class="tracking-wide font-semibold uppercase text-2xl mx-2 text-center">
          {{ $t('ways_to_join.bar_buddy.sign_up') }}
        </h2>
        <div v-if="formStatus === 'finished'">
          <div class="mx-auto container px-4 my-8 flex justify-center">
            <div class="bg-white rounded shadow-lg p-8 md:pr-48 text-lg flex items-center">
              <div class="rounded-full w-16 h-16 p-3 bg-pink-400 text-white">
                <Zondicon icon="checkmark-outline" class="fill-current w-10" />
              </div>
              <div class="ml-4">
                <h4 class="font-semibold text-xl">{{ $t('forms.success.heading') }}</h4>
                <span class="text-gray-700">{{ $t('forms.success.barbuddy') }}</span>
              </div>
            </div>
          </div>
        </div>
        <form v-if="formStatus !== 'finished'" @submit="submit" class="md:w-2/3 mx-4 md:mx-auto mt-8 md:my-12">
          <FormValidationMessage :errors="validationErrors" />
          <p class="form-element">
            <label class="required">{{ $t('forms.label.name') }}</label>
            <input v-model="form.name" :placeholder="$t('forms.placeholder.name')" type="text" required />
            <FormValidation :errors="validationErrors" name="name" />
          </p>
          <p class="form-element">
            <label class="required">{{ $t('forms.label.language') }}</label>
            <label class="radio">
              <input v-model="form.language" type="radio" value="dutch" />
              {{ $t('forms.label.languages.dutch') }}
            </label>
            <label class="radio">
              <input v-model="form.language" type="radio" value="english" />
              {{ $t('forms.label.languages.english') }}
            </label>
            <label class="radio">
              <input v-model="form.language" type="radio" value="no_preference" />
              {{ $t('forms.label.languages.no_preference') }}
            </label>
            <FormValidation :errors="validationErrors" name="language" />
          </p>
          <p class="form-element">
            <label class="required">{{ $t('forms.label.email') }}</label>
            <input v-model="form.email" :placeholder="$t('forms.placeholder.email')" type="email" required />
            <FormValidation :errors="validationErrors" name="email" />
          </p>
          <p class="form-element">
            <label>{{ $t('forms.label.phone_number') }}</label>
            <input v-model="form.phone_number" :placeholder="$t('forms.placeholder.phone_number')" type="text" />
            <FormValidation :errors="validationErrors" name="phone_number" />
          </p>
          <p class="form-element">
            <label>{{ $t('forms.label.pronouns') }}</label>
            <input v-model="form.pronouns" :placeholder="$t('forms.placeholder.pronouns')" type="text" />
            <FormValidation :errors="validationErrors" name="pronouns" />
          </p>
          <p class="form-element">
            <label class="required">{{ $t('forms.label.barbuddy') }}</label>
            <label class="radio">
              <input v-model="form.barbuddy" type="radio" value="no_preference" />
              {{ $t('forms.label.languages.no_preference') }}
            </label>
            <label v-for="buddy in barbuddies" :key="buddy.name" class="radio">
              <input v-model="form.barbuddy" :value="buddy.name" :checked="buddy.selected" type="radio" />
              {{ buddy.name }}
            </label>
            <FormValidation :errors="validationErrors" name="barbuddy" />
          </p>
          <p class="form-element">
            <label>{{ $t('forms.label.remarks') }}</label>
            <textarea v-model="form.remarks" :placeholder="$t('forms.placeholder.remarks')"></textarea>
            <FormValidation :errors="validationErrors" name="remarks" />
          </p>
          <div id="recaptcha" />
          <p class="mt-8 md:my-8 text-right">
            <button :disabled="formStatus === 'loading'" type="submit" class="button-pink">
              {{ formStatus === 'loading' ? $t('forms.buttons.loading') : $t('forms.buttons.sign_up') }}
            </button>
          </p>
        </form>
      </div>
    </section>
  </div>
</template>

<script>
import Zondicon from 'vue-zondicons'
import ReMemberForm from '~/modules/ReMemberForm'
import Header from '~/components/Header'
import FormValidation from '~/components/Form/FormValidation'
import FormValidationMessage from '~/components/Form/FormValidationMessage'

export default {
  components: {
    Header,
    Zondicon,
    FormValidation,
    FormValidationMessage
  },
  data() {
    return {
      barbuddies: Object.keys(this.$t('barbuddies')).map(name => {
        return {
          name,
          bio: this.$t('barbuddies.' + name),
          readMore: false
        }
      }),
      form: {
        name: '',
        language: this.$i18n.locale === 'nl' ? 'dutch' : 'english',
        email: '',
        phone_number: '',
        pronouns: '',
        barbuddy: 'no_preference',
        remarks: ''
      },
      validationErrors: {},
      formStatus: 'start'
    }
  },
  methods: {
    meetWith(buddy) {
      this.form.barbuddy = buddy.name
      window.scrollTo({ top: document.getElementById('form').offsetTop, behavior: 'smooth' })
    },
    readMore(buddy) {
      buddy.readMore = !buddy.readMore
    },
    submit(event) {
      event.preventDefault()

      this.formStatus = 'loading'

      new ReMemberForm('barbuddy')
        .submit(this.form)
        .then(() => {
          this.formStatus = 'finished'
          window.scrollTo({ top: document.getElementById('form').offsetTop, behavior: 'smooth' })
        })
        .catch(validationError => {
          this.formStatus = 'validation-error'
          this.validationErrors = validationError.errors()
          window.scrollTo({ top: document.getElementById('form').offsetTop, behavior: 'smooth' })
        })
    }
  }
}
</script>

<style>
.clamp-lines {
  display: -webkit-box;
  -webkit-line-clamp: 5;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.white-gradient {
  background-image: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1));
}
</style>
