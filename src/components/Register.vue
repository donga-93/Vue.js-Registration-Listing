<template>
  <div class="register">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-sm-12 col-md-8 col-lg-6">
          <div class="card">
            <div class="card-header">
              <div class="card-title">რეგისტრაციის ფორმის</div>
            </div>
            <div class="card-body">
              <form novalidate @submit.prevent="registerUser()">
                <div class="form-group">
                  <input
                    type="text"
                    :class="`form-control ${
                      errors.username ? 'is-invalid' : ''
                    }`"
                    placeholder="სახელი"
                    v-model="username"
                  />
                  <div class="invalid-feedback">{{ errors.username }}</div>
                </div>
                <div class="form-group">
                  <input
                    type="text"
                    :class="`form-control ${
                      errors.usersurname ? 'is-invalid' : ''
                    }`"
                    placeholder="გვარი"
                    v-model="usersurname"
                  />
                  <div class="invalid-feedback">{{ errors.usersurname }}</div>
                </div>
                <div class="form-group">
                  <input
                    type="email"
                    :class="`form-control ${errors.email ? 'is-invalid' : ''}`"
                    placeholder="მეილი"
                    v-model="email"
                  />
                  <div class="invalid-feedback">{{ errors.email }}</div>
                </div>
                <div class="form-group">
                  <input
                    type="password"
                    :class="`form-control ${
                      errors.password ? 'is-invalid' : ''
                    }`"
                    placeholder="პაროლი"
                    v-model="password"
                  />
                  <div class="invalid-feedback">{{ errors.password }}</div>
                </div>
                <div class="form-group">
                  <input
                    type="password"
                    :class="`form-control ${
                      errors.password2 ? 'is-invalid' : ''
                    }`"
                    placeholder="პაროლის გამეორება"
                    v-model="password2"
                  />
                  <div class="invalid-feedback">{{ errors.password2 }}</div>
                </div>
               <div class="form-group">
                  <input
                    type="date"
                    :class="`form-control ${
                      errors.username ? 'is-invalid' : ''
                    }`"
                    placeholder="Date of birth"
                    v-model="dob"
                  />
                  <div class="invalid-feedback">{{ errors.dob }}</div>
                </div>
                <button class="btn btn-outline-success form-control">
                  რეგისტრაცია
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import validateRegisterInput from "../validation/validateRegisterInput";
export default {
  data() {
    return {
      username: "",
      usersurname: "",
      email: "",
      password: "",
      password2: "",
      dob: "",
      errors: {},
      users: [],
    };
  },
  methods: {
    registerUser() {
      let user = {
        username: this.username,
        usersurname: this.usersurname,
        email: this.email,
        password: this.password,
        password2: this.password2,
        dob: this.dob
      };

      const { isInvalid, errors } = validateRegisterInput(user);

      if (isInvalid) {
        this.errors = errors;
      } else {
        this.errors = {};
        // store user in local storage
        if (localStorage.users) {
          let lsUsers = localStorage.users;
          this.users = JSON.parse(lsUsers);
        }
        this.users.push(user);
        localStorage.setItem("users", JSON.stringify(this.users));
        this.username = "";
        this.usersurname = "";
        this.email = "";
        this.password = "";
        this.password2 = "";
        this.dob = "";
        this.$router.push("/login");
      }
    },
  },
};
</script>

<style>
.register {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
}
</style>
