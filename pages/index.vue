<template>
  <!-- グリッドシステムを使うために必要。display:flexの意味を持つ wrap属性が肝？？-->
  <v-layout column justify-center align-center wrap>
    <!-- 12分割のグリッドシステムを採用している。xsは600px未満でスマホ、smは600～960pxでipad(768px) -->
    <v-flex xs12 sm8 md6>
      <div class="card-wrapper-flex">
        <Item v-for="work in works" :key="work.sys.id" :work="work" />
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import Item from '@/components/Item'
import { createClient } from '~/plugins/contentful.js'

const client = createClient()

export default {
  components: {
    Item
  },
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type':'work',
        order: '-sys.createdAt'
      })
    ]).then(([works]) => {
      return {
        works: works.items
      }
    })
  }
}
</script>
