<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        pwa-lab
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
        <button class="button--green" @click="installPWA">
          + Install App
        </button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  mounted () {
    window.addEventListener('beforeinstallprompt', function (event) {
      // not show the default browser install app prompt
      event.preventDefault()

      // add the banner here or make it visible
      alert('Please for subscribe!!!')

      // save the event to use it later
      // (it has the important prompt method and userChoice property)
      window.promptEvent = event
    })
    window.addEventListener('appinstalled', (evt) => {
      // Log install to analytics
      alert('Thx for subscribe!!!')
    })
  },
  methods: {
    installPWA () {
      if (process.client) {
      // show the install app prompt
        window.promptEvent.prompt()

        // handle the Decline/Accept choice of the user
        window.promptEvent.userChoice.then(function (choiceResult) {
        // hide the prompt banner here
        // …

          if (choiceResult.outcome === 'accepted') {
            console.log('mm User accepted the A2HS prompt')
          } else {
            console.log('mm User dismissed the A2HS prompt')
          }

          window.promptEvent = null
        })
      }
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
