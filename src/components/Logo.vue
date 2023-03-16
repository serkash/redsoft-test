<template>
  <a href="/" class="logo">
    <img src="@/assets/logo.png" class="logo__image" :alt="title">
  </a>
</template>

<script>

export default {
  name: 'LogoVue',
  data () {
    return {
      title: 'The FAMOUS'
    }
  }
}

</script>