<template lang="pug">
  div(v-if="track && track.id")
    .container
      .columns
        .column.is-3.has-text-centered
          figure.media-left
            img.image(:src="track.album.images[0].url")

        .column.is-8
          .panel
            .panel-heading
              h1.title {{track.name}}
            .panel-block
              article.media
                .media-content
                  .content
                    ul(v-for="(v, k) in track")
                      li
                        strong {{k}}:&nbsp;
                        span {{v}}
</template>

<script>
import trackService from '~/plugins/track'

export default {
  components: {},
  data () {
    return {
      track: {}
    }
  },
  head () {
    return {
      title: this.track.name
    }
  },
  asyncData ({ params }) {
    const id = params.Id

    return trackService.getById(id)
      .then((track) => {
        return { track }
      })
  }
}
</script>

<style lang="scss" scoped>
  .column {
    padding: 20px;
  }

  .button-bar {
    margin-top: 20px;
  }
</style>
