<template lang='pug'>
  span(class="btn--select-wrapper" :class="[active ? 'active' : '']")
    btn(:value="value")
</template>

<script>
import Btn from '@nylira/vue-button'
export default {
  name: 'toggle-btn',
  components: {
    Btn
  },
  props: ['value', 'active']
}
</script>

<style lang="stylus">
@require '~@/styles/variables.styl'

.btn--select-wrapper.active
  .ni-btn-value
    color app-bg

  .ni-btn-container
    background txt
</style>
