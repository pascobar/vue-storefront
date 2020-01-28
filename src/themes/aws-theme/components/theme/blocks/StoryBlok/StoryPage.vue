<template>
  <div class="storyblok" v-editable="blok">
    <story-content v-for="item in blok.body" :item="item" :key="item._uid" />
  </div>
</template>

<script>
import StoryContent from 'theme/components/theme/blocks/StoryBlok/StoryContent'

export default {
  name: 'StoryPage',
  components: {
    'story-content': StoryContent
  },
  props: ['blok']
}
</script>
