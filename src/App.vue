<template lang="pug">
  v-app
    v-toolbar.purple.darken-2
      v-toolbar-title.white--text Угадай номер!
    main
      v-container(fluid).grey.lighten-3
        router-view
</template>

<script>
export default {
  name: 'app'
}
</script>

<style scoped>
</style>
