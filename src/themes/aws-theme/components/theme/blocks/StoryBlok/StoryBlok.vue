<template>
  <page :blok="story.content" :is="story.content.component" />
</template>

<script>
import StoryblokClient from 'storyblok-js-client'
import StoryPage from 'theme/components/theme/blocks/StoryBlok/StoryPage'

const token = 'qiHuthhHxbNmePMSfuGeGwtt'

let storyapi = new StoryblokClient({
  accessToken: token
})

export default {
  name: 'StoryBlok',
  components: {
    'page': StoryPage
  },
  data () {
    return {
      story: {
        content: {
          body: []
        }
      }
    }
  },
  async created () {
    window.storyblok.init({
      accessToken: token
    })
    window.storyblok.on('change', () => {
      this.getStory('home', 'draft')
    })
    window.storyblok.pingEditor(() => {
      if (window.storyblok.isInEditor()) {
        this.getStory('home', 'draft')
      } else {
        this.getStory('home', 'published')
      }
    })
  },
  methods: {
    getStory (slug, version) {
      storyapi.get('cdn/stories/' + slug, {
        version: version
      })
        .then((response) => {
          this.story = response.data.story
        })
        .catch((error) => {
          console.log(error);
        })
    }
  }
}
</script>
