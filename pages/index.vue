<template>
  <div class="row justify-content-md-center mt-4">
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Password:" label-for="input-2">
        <b-form-input
          id="input-1"
          v-model="form.password"
          type="password"
          placeholder="Enter password"
          required
        ></b-form-input>

      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          email: '',
          password: ''
        },
        show: true
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()

        const url = 'http://localhost:8080/api/login'
        this.$axios
          .$get(url, {
            headers: {
              // Accept: "application/text",
              // "Access-Control-Allow-Origin" : "true",
              "Content-Type": "application/text;charset=UTF-8",
              // "Authorization": "Basic " + (Buffer.from(this.email + ":" + this.password).toString('base64'))
            },
          })
          .then((data) => {
            console.log(data);
            alert(data)
          });
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.password = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>
