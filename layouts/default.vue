<template>
  <v-app id="inspire">
    <!-- ナビゲーションサイドバー -->
    <v-navigation-drawer v-model="drawer" app>
      <!-- プロフィール写真 -->
      <v-img src="https://chobimusic.com/wp-content/uploads/2020/02/about-me-square.jpg" height="200px"></v-img>
      <!-- リンクリスト -->
      <v-list dense>
        <v-list-item link to="/">
          <v-list-item-action>
            <font-awesome-icon :icon="['fas', 'home']" />
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <a href="https://masaru-portfolio.netlify.com/" target="_blank">
          <v-list-item link>
            <v-list-item-action>
              <font-awesome-icon :icon="['fas', 'user']" />
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>Profile</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </a>
        <a href="https://twitter.com/masaru_pg" target="_blank">
          <v-list-item link>
            <v-list-item-action>
              <font-awesome-icon :icon="['fab', 'twitter']" />
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>Twitter</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </a>
        <a href="https://chobimusic.com/" target="_blank">
          <v-list-item link>
            <v-list-item-action>
              <font-awesome-icon :icon="['fas', 'pen']" />
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>Blog</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </a>
      </v-list>
      <vs-input icon="search" placeholder="Search" v-model="keyword" @keypress.enter="$router.push('/search/'+keyword)" style="margin-left:15px"/>
    </v-navigation-drawer>
    <!-- ヘッドバー darkで文字が白になる。 -->
    <v-app-bar app color="blue" dark hide-on-scroll>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <!-- ブログタイトル -->
      <nuxt-link to="/" style="color:white"><v-toolbar-title><font-awesome-icon :icon="['fas', 'home']" /> chobilog</v-toolbar-title></nuxt-link>
    </v-app-bar>

    <!-- v-content内はサイドバーの動きと連動する -->
    <v-content id="top">
      <!-- v-container内はfluid属性で左右一杯に広げたりできる。 -->
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <!-- <v-bottom-navigation scroll-target="#scroll-area-1" hide-on-scroll absolute horizontal style="color:blue">
      <v-btn text color="deep-purple accent-4">
        <span>&copy; chobilog</span>
        <v-icon>mdi-history</v-icon>
      </v-btn>
    </v-bottom-navigation> -->
    <!-- appを消すと固定表示消える。スクロール機能はつかないぽい。 -->
    <v-footer color="blue" hide-on-scroll>
      <a href="#top"><span class="white--text">&copy; chobilog</span></a>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      drawer: false
    }
  }
}
</script>
