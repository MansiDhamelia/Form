<template>
  <div class="container">
    <h1>Form</h1>

    <div class="items">
      <label for="name">Name</label>
      <input
        type="text"
        v-model="user.name"
        name="name"
        placeholder="Enter name"
        :class="{ 'is-invalid': submitStatus && $v.user.name.$error }"
      />
      <div v-if="submitStatus && $v.user.name.$error" class="invalid-msg">
        <span v-if="!$v.user.name.required">Field is required</span>
        <span v-else-if="!$v.user.name.minLength"
          >Name must be at least 4 character.</span
        >
      </div>
    </div>

    <div class="items">
      <label for="address">Address</label>
      <input
        type="text"
        v-model="user.address"
        name="address"
        placeholder="Enter address"
        :class="{ 'is-invalid': submitStatus && $v.user.address.$error }"
      />
      <div v-if="submitStatus && $v.user.address.$error" class="invalid-msg">
        <span v-if="!$v.user.address.required"> Field is required</span>
        <span v-if="!$v.user.address.maxLength">
          Address have at most 50 letters.</span
        >
      </div>
    </div>

    <div class="items">
      <label>Contact</label>
      <input
        type="number"
        placeholder="Enter mobile number"
        name="contact"
        v-model="user.contact"
        :class="{ 'is-invalid': submitStatus && $v.user.contact.$error }"
      />
      <div v-if="submitStatus && $v.user.contact.$error" class="invalid-msg">
        <span v-if="!$v.user.contact.required">Field is required.</span>
        <span v-if="!$v.user.contact.minLength"
          >Contact must be at least 10 number.</span
        >
      </div>
    </div>

    <div class="items">
      <label for="email">Email</label>
      <input
        type="text"
        v-model="user.email"
        name="email"
        placeholder="Enter email"
        :class="{ 'is-invalid': submitStatus && $v.user.email.$error }"
      />
      <div v-if="submitStatus && $v.user.email.$error" class="invalid-msg">
        <span v-if="!$v.user.email.required">Field is required</span>
        <span v-if="!$v.user.email.email">Email is invalid.</span>
      </div>
    </div>

    <div class="items">
      <label for="password">Password</label>
      <input
        type="password"
        v-model="user.password"
        name="password"
        id="password"
        placeholder="Enter password"
        :class="{ 'is-invalid': submitStatus && $v.user.password.$error }"
      />
      <div v-if="submitStatus && $v.user.password.$error" class="invalid-msg">
        <span v-if="!$v.user.password.required">Field is required</span>
        <span v-if="!$v.user.password.minLength"
          >Password must be at least 5 character.</span
        >
      </div>
    </div>

    <div class="items">
      <label for="confirmPassword">Confirm Password</label>
      <input
        type="password"
        v-model="user.confirmPassword"
        name="confirmPassword"
        placeholder="Reenter Password"
        :class="{
          'is-invalid': submitStatus && $v.user.confirmPassword.$error,
        }"
      />
      <div
        v-if="submitStatus && $v.user.confirmPassword.$error"
        class="invalid-msg"
      >
        <span v-if="!$v.user.confirmPassword.required">Field is required</span>
        <span v-if="!$v.user.confirmPassword.sameAsPassword"
          >Password must match.</span
        >
      </div>
    </div>
    <button class="btn" @click="submit">Submit</button>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  email,
  sameAs,
} from "vuelidate/lib/validators";

export default {
  data() {
    return {
      user: {
        name: "",
        lastName: "",
        address: "",
        contact: "",
        email: "",
        password: "",
        confirmPassword: "",
      },
      submitStatus: false,
    };
  },
  validations: {
    user: {
      name: {
        required,
        minLength: minLength(4),
      },
      address: {
        required,
        maxLength: maxLength(50),
      },
      contact: {
        required,
        minLength: minLength(10),
      },
      email: { required, email },
      password: { required, minLength: minLength(5) },
    
    confirmPassword: { required, sameAsPassword: sameAs("password") },
    },
  },
  methods: {
    submit(e) {
      console.log(this.submitStatus);
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        alert("success!!");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.invalid-msg{
  color: red;
}
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin-left: 300px;
}
.items {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.btn {
  width: 100px;
  height: 30px;
  margin: 10px 0px;
}
input {
  margin: 10px 0px;
  height: 30px;
  width: 50%;
}

</style>
