<!-- 作品情報を取得する -->

<template>
  <div class="article">
    <!-- カテゴリーリンク -->
    <div class="article-main-img">
      <nuxt-link :to="{ name: 'category-id', params: { id: work.fields.category.sys.id } }">
        <div class="tag">
          <font-awesome-icon :icon="['fas', 'paperclip']" /> {{ work.fields.category.fields.name }}
        </div>
      </nuxt-link>
      <img :src=" work.fields.image.fields.file.url " style="width:60%;margin-top:10px;border-radius:5px;">
    </div>
    <!-- タイトル -->
    <h1 class="text-left text-4xl article-title">{{ work.fields.title }}</h1>
    <!-- サブタイトル -->
    <!-- <p class="text-left text-sm">{{ work.fields.subtitle }}</p> -->
    <!-- v-htmlディレクティブはデータをHTML形式で表示してくれる -->
    <div class="content" v-html="$md.render(work.fields.content)"></div>
    <div class="flex" style="margin:auto">
      <li
        v-for="tag in work.fields.tag"
        :key="tag.sys.id"
        style="list-style: none;text-align:center;"
      >
        <v-chip class="ma-2" label>
          <nuxt-link :to=" '/tag/' + tag.sys.id ">
            {{ tag.fields.name }}
          </nuxt-link>
        </v-chip>
      </li>
    </div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'

const client = createClient()
export default { 
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.slug': params.slug
      })
    ]).then(([works]) => {
      return {
        work: works.items[0]
      }
    })
  }
}
</script>
