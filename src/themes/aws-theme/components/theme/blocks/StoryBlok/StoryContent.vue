<template>
  <div v-editable="item" class="storyblok__block">
      <h2 class="storyblok__heading" 
          :if="item.headline" 
          v-html="item.headline" 
          :class="[item.row_style ? item.row_style : '']">
      </h2>
      <div class="storyblok__img" 
           :if="item.image"
           :class="[item.column_style ? item.column_style : '']" 
           :style="[item.image_position ? {'float': item.image_position} : '']"
      >
        <img :src="item.image" :alt="item.icon_alt_text">
      </div>
      <div class="storyblok__content">
        <h3 :if="item.subheadline">
          {{item.subheadline}}
        </h3>
        <div class="storyblok__text" :if="item.text" v-html="item.text"></div>
        <div class="storyblok__actions">
          <div class="storyblok__action"
               v-for="button in item.buttons" 
               :key="button._uid" 
               :class="[button.style ? button.style : '']"
          >
            <a :if="button.link.url" :href="button.link.url" target="_blank">{{button.text}}</a>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'StoryContent',
  props: ['item']
}
</script>

<style lang="scss" scoped>
  .pl-40 {
    padding-left: 40px;
  }

  .pr-40 {
    padding-right: 40px;
  }

  .mt-40 {
    margin-top: 40px;
  }

  .storyblok {
    &__block {
      &:after {
        clear: both;
        content: '';
        display: block;
      }
    }

    &__action {
      a {
        background-color: #e91e63;
        border-radius: 3px;
        color: white;
        font-size: 13px;
        padding: 11px 30px;
        text-transform: uppercase;
      }
    }
  }
</style>