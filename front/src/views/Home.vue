<template>
  <div class="login mt-5">
    <div class="card">
      <div class="card-header">
       Contact Form
      </div>
      <div class="card-body">
        <form>
          <div class="form-group">
            <label for="email">Name</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': errors.name }"
              id="name"
              v-model="details.name"
              placeholder="Enter name"
            />
            <div class="invalid-feedback" v-if="errors.name">
              {{ errors.name[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="email">Email address</label>
            <input
              type="email"
              class="form-control"
              :class="{ 'is-invalid': errors.email }"
              id="email"
              v-model="details.email"
              placeholder="Enter email"
            />
            <div class="invalid-feedback" v-if="errors.email">
              {{ errors.email[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="email">Gender</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': errors.gender }"
              id="gender"
              v-model="details.gender"
              placeholder="Enter gender"
            />
          </div>
          <div class="form-group">
            <label for="email">Content</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': errors.content }"
              id="content"
              v-model="details.content"
              placeholder="Enter content"
            />
          
          </div>
          <button type="button" @click="register" class="btn btn-primary">
            Register
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Home",

  data: function() {
    return {
      details: {
        name: null,
        email: null,
        password: null,
        password_confirmation: null,
        gender: null,
        content: null
      }
    };
  },

  computed: {
    ...mapGetters(["errors"])
  },

  mounted() {
    this.$store.commit("setErrors", {});
  },

  methods: {
    ...mapActions("auth", ["sendRegisterRequest"]),

    register: function() {
      this.sendRegisterRequest(this.details).then(() => {
        this.$router.push({ name: "Home" });
      });
    }
  }
};
</script>
