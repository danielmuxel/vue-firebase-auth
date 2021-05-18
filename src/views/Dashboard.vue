<template>
  <h1>Dashboard</h1>
  <div v-if="user">
    {{ user }}
    Hello {{ user.data.displayName }}, happy to see you!
  </div>
  <div v-else>
    You should not be here...
  </div>
</template>

<script>
import { mapGetters } from "vuex"
export default {
  computed: {
    ...mapGetters({
      user: "user"
    })
  }
}
</script>