<template>
  <form @submit.prevent="handleSubmit">
    <div class="field">
      <label class="label">Email</label>
      <div class="control has-icons-left has-icons-right">
        <input
          class="input"
          type="email"
          v-model="formMail"
          placeholder="Email input"
        />
        <span class="icon is-small is-left">
          <fa icon="envelope" />
        </span>
        <span class="icon is-small is-right" v-if="emailInvalid">
          <fa icon="exclamation-triangle" />
        </span>
      </div>
      <p class="help is-danger" v-if="emailInvalid">This email is invalid</p>
    </div>

    <div class="field">
      <label class="label">Subject</label>
      <input class="input" type="text" placeholder="Subject" v-model="formSubject" />
    </div>

    <div class="field">
      <label class="label">Message</label>
      <div class="control">
        <textarea
          class="textarea"
          placeholder="Textarea"
          v-model="formContent"
        ></textarea>
      </div>
    </div>

    <div class="field is-grouped">
      <div class="control">
        <button class="button is-link">Submit</button>
      </div>
      <div class="control">
        <button class="button is-link is-light">Cancel</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: 'MailForm',
  data() {
    return {
      formMail: '',
      formSubject: '',
      formContent: '',
      emailInvalid: false,
    }
  },
  methods: {
    handleSubmit() {
      console.log(this.formMail, this.formSubject, this.formContent)
      this.formMail = ''
      this.formSubject = ''
      this.formContent = ''
    },
  },
}
</script>
