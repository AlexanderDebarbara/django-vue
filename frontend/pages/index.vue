<template>
    <notas-list/>
</template>

<script>
import notasList from '~/components/notas-list.vue'
import Vuex from 'vuex'

export default {
  layout: 'complex',
  components: {
    notasList
  },
  data () {
    return {}
  }
}
</script>

<style>
</style>
