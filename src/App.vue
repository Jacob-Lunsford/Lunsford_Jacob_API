<template>
  <section class="section">
    <div class="container">

      <h1 class="title has-text-primary">
        Random Dog Viewer
      </h1>

      <p class="subtitle">
        Retrieve random dog images.
      </p>

      <div v-if="loading">
        <h3>Loading data...</h3>
      </div>

      <div v-else-if="errorMessage">
        <h3 class="has-text-danger">
          {{ errorMessage }}
        </h3>
      </div>

      <div v-else>
        <div class="box">
          <img
            :src="dogImage"
            alt="Random Dog"
            class="dog-image"
          >
        </div>
      </div>

      <div class="buttons is-centered">
        <button
          class="button is-primary"
          @click="getDogImage"
        >
          New dog image
        </button>
      </div>

    </div>
  </section>
</template>

<script>
export default {

  data() {
    return {

      dogImage: '',

      loading: false,

      errorMessage: ''

    }
  },

  methods: {

    async getDogImage() {

      this.loading = true
      this.errorMessage = ''

      try {

        const response = await fetch(
          'https://dog.ceo/api/breeds/image/random'
        )

        const data = await response.json()

        this.dogImage = data.message

      }
      catch (error) {

        this.errorMessage =
          'Unable to retrieve dog image.'

      }
      finally {

        this.loading = false

      }

    }

  },

  mounted() {

    this.getDogImage()

  }

}
</script>

<style>
body {
  background-color: #f5f5f5;
}

.container {
  text-align: center;
}

.dog-image {
  width: 500px;
  max-width: 100%;
  border: 4px solid #3273dc;
  border-radius: 10px;
}

.box {
  margin-bottom: 20px;
}
</style>