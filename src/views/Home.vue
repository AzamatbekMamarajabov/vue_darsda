<template>
  <div class="home">
    <Complex />
  </div>
</template>

<script>
// @ is an alias to /src
import Complex from '@/components/Complex.vue'

export default {
  name: 'Home',
  components: {
    Complex
  }
}
</script>
