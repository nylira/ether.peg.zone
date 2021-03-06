<template lang="pug">
.modal-wrapper
  .modal-person
    img.avatar(:src='portrait(person.slug)')
    .text
      .name {{ person.name }}
      .title {{ person.groups[group] }}
      .bio {{ person.bio }}
    .links
      a(v-if='person.ids.email', :href="'mailto:' + person.ids.email + '@tendermint.com'", target='_blank')
        i.material-icons mail_outline
        span.label {{ person.ids.email }}@tendermint.com
      a(v-if='person.ids.github', :href="'https://github.com/' + person.ids.github", target='_blank')
        i.material-icons code
        span.label github.com/{{ person.ids.github }}
      a(v-if='person.ids.keybase', :href="'https://keybase.io/' + person.ids.keybase", target='_blank')
        i.material-icons vpn_key
        span.label keybase.io/{{ person.ids.keybase }}
      a(v-if='person.ids.linkedin', :href="'https://www.linkedin.com/in/' + person.ids.linkedin", target='_blank')
        i.material-icons contact_mail
        span.label {{ person.name }}
      a(v-if='person.ids.twitter', :href="'https://twitter.com/' + person.ids.twitter", target='_blank')
        i.material-icons question_answer
        span.label @{{ person.ids.twitter }}
      a(v-if='person.ids.website', :href="'http://' + person.ids.website", target='_blank')
        i.material-icons web
        span.label {{ person.ids.website }}
</template>

<script>
import { portrait } from 'scripts/cdn'
import disableScroll from 'disable-scroll'
export default {
  name: 'section-people',
  data: () => ({
    portrait: portrait
  }),
  mounted () {
    disableScroll.on()
  },
  beforeDestroy () {
    disableScroll.off()
  },
  props: ['person', 'group']
}
</script>

<style scoped lang="stylus">
@import '~variables'

.modal-wrapper
  position fixed
  top 0
  left 0
  width 100vw
  height 100vh
  z-index 100

  display flex
  align-items center
  justify-content center

  background hsla(0,0,0,0.5)
  backdrop-filter blur(0.5rem)

.modal-person
  max-width 360px
  width 100%
  background app-fg
  shadow()
  margin 0 0.5rem

  display flex
  align-items center
  flex-flow column
  position relative
  &:before
    display block
    position absolute
    top 0
    right 0

    width 4rem
    height 4rem
    display flex
    align-items center
    justify-content center

    content 'close'
    font-family 'Material Icons'
    font-size h3
    cursor pointer
    color link

  .avatar
    display block
    width 8rem
    margin 2rem 2rem 0
    border-radius 10rem

  .text
    text-align center
    padding 1rem 1.5rem 1.25rem

  .name
    color bright
    font-size h3

  .title
    font-size h5
    color dim
    margin-bottom 0.75rem

  .bio
    text-align left

  .links
    width 100%
    height 3rem
    display flex
    justify-content center
    background app-bg
    a
      flex 1

      display flex
      align-items center
      justify-content center

      color link

      &:hover
        color hover

      i.material-icons
        font-size h4
      .label
        display none

@media screen and (min-width: 360px)
  .modal-person
    margin 0 0.75rem
    .avatar
      width 9rem

@media screen and (min-width: 400px)
  .modal-person
    .avatar
      width 10rem

    .title
      margin-bottom 1.25rem

    .links a
      flex 0 0 60px
</style>
