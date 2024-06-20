<template>
  <div class="app">
    <form class="form" @submit.prevent="submitForm">
      <div class="kids">
        <div class="title">
          <h2>Contact Us</h2>
        </div>
        <div class="c1">
          <div>
            <label for="firstname">First Name* </label>
            <b-form-input
              v-model="firstName"
              required
              name="firstname"
            ></b-form-input>
          </div>
          <div class="sec">
            <label for="lastname">Last Name* </label>
            <b-form-input
              v-model="lastName"
              required
              name="lastname"
            ></b-form-input>
          </div>
        </div>

        <div class="c4">
          <label for="email">Email Adress * </label>
          <b-form-input
            v-model="emailAdress"
            required
            type="text"
            name="email"
          ></b-form-input>
        </div>
        <label class="c4" for="none"> Query Type *</label>
        <div class="c2">
          <div class="c3">
            <input
              type="radio"
              id="General Enquiry"
              value="General Enquiry"
              v-model="queryType"
            />
            <label for="General Enquiry">
              <span style="margin-left: 10px"> General Enquiry </span></label
            >
          </div>
          <div class="c3">
            <input
              type="radio"
              id="Support Request"
              value="Support Request"
              v-model="queryType"
            />
            <label for="Support Request"
              ><span style="margin-left: 10px">Support Request</span>
            </label>
          </div>
        </div>
        <div class="c4">
          <label for="email">Message * </label>
          <b-form-textarea
            id="message"
            name="message "
            v-model="message"
            placeholder=""
            rows="3"
            max-rows="6"
          ></b-form-textarea>
        </div>
        <div class="c4">
          <input
            type="checkbox"
            id="contactTeam"
            v-model="contactTeam"
            true-value="yes"
            false-value="no"
          />
          <label for="contactTeam"
            ><span style="margin-left: 10px">
              I consent to being contacted by the team*
            </span></label
          >
        </div>
        <div class="buttom-submit">
          <button type="submit">Submit Message</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
const WEB3FORMS_ACCESS_KEY = "2124074e-4cf9-4f96-9cc3-5b01da3c0e44";

export default {
  data() {
    return {
      firstName: "",
      lastName: "",
      emailAdress: "",
      queryType: [],
      message: "",
      contactTeam: "no",
    };
  },
  methods: {
    async submitForm() {
      const response = await fetch("https://api.web3forms.com/submit", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify({
          access_key: WEB3FORMS_ACCESS_KEY,
          firstName: this.firstName,
          lastName: this.lastName,
          emailAdress: this.emailAdress,
          queryType: this.queryType,
          message: this.message,
          contactTeam: this.contactTeam,
        }),
      });
      const result = await response.json();
      if (result.success) {
        console.log(result);
      }
      alert("Form submitted successfully!");
      window.location.reload();
    },
  },
};
</script>
<style>
.app {
  display: flex;
  justify-content: center;

  background: #4949914d;
}
.form {
  display: flex;
  flex-direction: column;
  border-radius: 10px;
  margin-top: 57px;
  margin-bottom: 100px;
  padding: 8%;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.212);
  background-color: #fff;
}
.kids {
  display: flex;

  flex-direction: column;
}
button {
  background: #069948f6;
  border: 0;
  padding: 16px 185px;

  color: white;
  border-radius: 5px;
  margin-top: 80px;
}
.buttom-submit {
  text-align: center;
}
.title h2 {
  color: black;
  font-size: 40px;
}
.c1 {
  display: flex;
  justify-content: space-between;
  margin-top: 50px;
}
.sec {
  margin-left: 60px;
}
.c2 {
  display: flex;
  justify-content: space-between;
}
.c3 {
  display: flex;
  justify-content: space-between;
  border-radius: 3px;
  border: 1px solid hsl(220, 2%, 74%);
  align-items: center;
  padding: 5px 30px;
}
.c4 {
  margin-top: 20px;
}
</style>
