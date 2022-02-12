<template>
  <div id="about-page" class="page-wrapper about-page content-page">
    <site-hero
      title="About Me"
      subtitle=":)"
      image="/uploads/about-hero.jpg"
    ></site-hero>
    <main-section theme="sidebar-right">
      <template v-slot:default>
        <div class="content"> 
        
        <article class="tile is-child box">
      
              <figure class="image is-1by1 ">
                <opti-image
                  :src="require('~/assets/uploads/logo.jpg').src"
                  :srcset="
                    require('~/assets/uploads/logo.jpg').srcSet
                  "
                />
              </figure>
              <br />
              <div class="content">
                <p>
                  Hi, I'm El Ghemary Farah, a Mathematics and applications bachelor student, 
                  and a self-thaught passionate programmer from Morocco.
                  I started this personal blog as an experiment, where I can share some random ideas. Enjoy :)
                </p>
              </div>
          </article>
          </div>
                
      </template>

      <template v-slot:sidebar>
        <h3 class="subtitle is-4">
          Latest Posts
        </h3>
        <posts-grid :per-row="1" :number="2" />
      </template>
    </main-section>
  </div>
</template>
<script>
import QuoteCard from '~/components/cards/QuoteCard'
export default {
  head() {
    return {
      title: `About | ${this.$siteConfig.siteName}`
    }
  },
  components: { QuoteCard }
}
</script>
