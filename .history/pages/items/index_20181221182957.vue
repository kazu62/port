<template>
  <section class="index">
    <card v-for="post in posts"
      :key="post.fields.path"
      :title="post.fields.title"
      :path="post.fields.path"
      :image="post.fields.image"
    />
  </section>
</template>

<script>
import Card from '~/components/card.vue'
import {createClient} from '~/plugins/contentful.js'

const client = createClient()
export default {
  transition: 'slide-left',
  components: {
    Card
  },
  async asyncData ({ env, params }) {
    return await client.getEntries({
      'content_type': process.env.CTF_PAGE_TYPE_ID,
    }).then(entries => {
      console.log(entry.sys)
      return {
        posts: entries.items
      }
    })
    .catch(console.error,
    console.log(process.env.CTF_PAGE_TYPE_ID),
    console.log('頑張って'))
  }
}
</script>

<style scoped>
.index {
  display: flex;
  flex-wrap: wrap;
}
</style>
