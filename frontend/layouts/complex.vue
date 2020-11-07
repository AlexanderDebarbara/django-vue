<template>
  <v-app>
    <v-content>
      <v-container fluid>
        <nuxt></nuxt>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  export default {
    components: {
    },
    data: () => ({
      layout: {
        drawer: true,
        drawerRight: true,
        right: null,
        left: null
      },
    })
  }
</script>
