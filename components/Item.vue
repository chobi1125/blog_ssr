<template>
  <div class="card-wrapper">
    <v-card class="mx-auto" width="300" height="400" :elevation="10">
      <div class="img-wrapper">
        <!-- カテゴリーリンク -->
        <nuxt-link :to="{ name: 'category-id', params: { id: work.fields.category.sys.id } }">
          <div class="tag">
            <font-awesome-icon :icon="['fas', 'paperclip']" /> {{ work.fields.category.fields.name }}
          </div>
        </nuxt-link>
        <img :src=" work.fields.image.fields.file.url " class="card-image">
      </div>
      <v-card-title class="black--text">
        <!-- タイトルリンク -->
        <nuxt-link :to=" '/work/' + work.fields.slug ">
          <h3 class="card-title">{{ work.fields.title }}</h3>
        </nuxt-link>
      </v-card-title>
      <v-card-text><div class="continue">{{ work.fields.date  }}</div></v-card-text>
      <div class="card-botton-wrapper">
        <li
          v-for="tag in work.fields.tag"
          :key="tag.sys.id"
        >
          <v-chip class="ma-2" label>
            <nuxt-link :to=" '/tag/' + tag.sys.id ">
              {{ tag.fields.name }}
            </nuxt-link>
          </v-chip>
        </li>
      </div>
    </v-card>
  </div>
</template>

<script>
// index.vueから変数workを取得
export default {
  props: ['work']
}
</script>
