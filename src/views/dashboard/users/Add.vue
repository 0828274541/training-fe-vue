<template>
  <v-container id="user-add" fluid tag="section">
    <base-v-component heading="Users" link="components/users" />
    <v-col class="text-left">
        <v-btn id="myButton" color="primary" class="mb-5" to="/users/list"
          >CLick to view user list!</v-btn
        >
    </v-col>
    <v-row>
      <v-col cols="12" md="12">
        <base-material-card
          color="success"
          icon="mdi-email"
          title="USER ADD FORM"
          class="px-5 py-3"
        >
          <form
                    ref="userForm"
                    class="mt-5"
                    id="app"
                    data-vv-scope="form-1"
                  >
                    <v-text-field
                      color="secondary"
                      v-model="firstname"
                      v-validate="'required'"
                      :error-messages="errors.collect('form-1.required')"
                      data-vv-name="firstname"
                      name="firstname"
                      label="First Name..."
                      prepend-icon="mdi-face"
                    />
                    <v-text-field
                      color="secondary"
                      v-model="lastname"
                      v-validate="'required'"
                      :error-messages="errors.collect('form-1.required')"
                      data-vv-name="lastname"
                      name="lastname"
                      label="Last Name..."
                      prepend-icon="mdi-face-woman "
                    />

                    <v-text-field
                      color="secondary"
                      v-model="username"
                      v-validate="'required'"
                      :error-messages="errors.collect('form-1.required')"
                      data-vv-name="required"
                      name="username"
                      label="Username..."
                      prepend-icon="mdi-account"
                    />

                    <v-text-field
                      class="mb-8"
                      color="secondary"
                      v-model="password"
                      v-validate="'required'"
                      :error-messages="errors.collect('form-1.required')"
                      data-vv-name="required"
                      name="password"
                      label="Password..."
                      prepend-icon="mdi-lock-outline"
                    />
                    <v-select
                      class="mb-8"
                      color="secondary"
                      v-model="role"
                      v-validate="'required'"
                      :items="roles"
                      item-text="role_text"
                      item-value="role_value"
                      label="Roles"
                      :error-messages="errors.collect('form-1.required')"
                      data-vv-name="required"
                      prepend-icon="mdi-airplane"
                    ></v-select>
                    <v-checkbox :input-value="true" color="secondary">
                      <template v-slot:label>
                        <span class="text-no-wrap">I agree to the&nbsp;</span>
                        <a class="secondary--text ml-6 ml-sm-0" href="#">
                          terms and conditions </a
                        >.
                      </template>
                    </v-checkbox>
            <v-card-actions class="pl-0">
              <v-btn
                color="success"
                min-width="100"
                @click.prevent="validateForm('form-1')"
              >
                Submit
              </v-btn>
            </v-card-actions>
                  </form>
        </base-material-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
const { usersApi } = require("../../../apis");

export default {
  name: "DashboardUserAddForms",

  $_veeValidate: {
    validator: "new",
  },
    data() {
    return {
      firstname: "",
      lastname: "",
      password: "",
      username: "",
      roles: [
        { role_text: "contributor", role_value: "contributor" },
        { role_text: "normal", role_value: "normal" }
        ]
    }
  },
  methods: {
    validateForm(scope) {
      this.$validator.validateAll(scope).then(async (result) => {
        if (result) {
          const result2 = await usersApi.addUser({
            firstName: this.firstname,
            lastName: this.lastname,
            username: this.username,
            password: this.password,
            roleCreate: this.role
          });
          if (result2.data.code === 200) {
            this.$notificate.showMessage({
              content: result2.data.message,
              color: "info",
            });
             this.$router.push("/users/list");
          } else {
            this.$notificate.showMessage({
              content: result2.data.message,
              color: "info",
            });
          }
        }
      });
    },
  },
};
</script>
