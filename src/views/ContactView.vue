<template>
  <div class="contact-view view-container">
    <p class="contact-head primary-element">Contact Me</p>
    <p class="p">If you have any question feel free to contact</p>
    <div class="form-error-container" v-if="formErrors">
      <span class="close-error-list" @click="formErrors = !formErrors">
        <font-awesome-icon icon="fa-solid fa-xmark" />
      </span>
      <span class="error" v-for="error in formErrors" :key="error.id">
        {{ error }}
        <br />
      </span>
    </div>
    <div class="success" v-if="msgSent">
      <span @click="msgSent = !msgSent">
        <font-awesome-icon icon="fa-solid fa-xmark" />
      </span>
      <span class="sent">{{ msgSent }}</span>
    </div>
    <div class="form-container">
      <form
        name="contact"
        method="POST"
        data-netlify="true"
        data-netlify-honeypot="bot-field"
      >
        <input
          type="text"
          name="name"
          class="form-control"
          placeholder="Name"
          v-model="username"
        />
        <input
          type="email"
          name="email"
          class="form-control"
          placeholder="Email"
          v-model="email"
          :disabled="!username"
        />
        <input
          type="text"
          name="subject"
          class="form-control"
          placeholder="Subject"
          v-model="subject"
          :disabled="!email || !username"
        />
        <textarea
          type="text"
          name="message"
          class="form-control"
          cols="30"
          rows="10"
          placeholder="Your Message"
          v-model="msg"
          :disabled="!email || !username"
        ></textarea>
        <button type="submit" class="btn">Send Message</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "contactView",
  data: function () {
    return {
      username: "",
      email: "",
      subject: "",
      msg: "",
      formErrors: null,
      msgSent: null,
    };
  },
  methods: {
    checkError: function () {
      this.formErrors = [""];
      if (!this.username) {
        this.formErrors.push("User name can't be empty");
      } else if (this.username.length < 4) {
        this.formErrors.push("User name can't be less than 8 characters");
      }
      if (!this.email) {
        this.formErrors.push("Email can't be empty");
      }
      if (!this.msg) {
        this.formErrors.push("message can't be empty");
      } else if (this.msg.length < 30) {
        this.formErrors.push("message can't be less than 30 characters");
      }
      if (this.formErrors.length == 1) {
        this.formErrors = null;
        this.msgSent = "We Received your message";
        this.username = "";
        this.email = "";
        this.subject = "";
        this.msg = "";
      }
    },
  },
};
</script>
