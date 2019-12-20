<template>
  <div class="container">
    <div>
      <logo />
      <h2 class="title">
        otohaba
      </h2>
      <h2 class="subtitle">
        音感を鍛えよう
      </h2>
      <p class="notice">
        ※スピーカーをオンにしてください
      </p>
      <div class="links">
        <nuxt-link to="/stanby" class="button--grey">
          スタート
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
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
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 270;
  font-size: 80px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 22px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.notice {
  font-size: 5px;
}
</style>
