<template>
  <Layout>
    <div class="container has-text-centered">
      <h1 class="title is-family-secondary">
        Collections
      </h1>
      <hr>
      <br>
      <p v-if="!collections.length">
        No collections available.
      </p>
      <div
        v-if="collections.length"
        class="columns is-multiline">
        <div
          v-for="({ node: collection }) in collections"
          :key="collection.id"
          class="column is-4">
          <div class="card">
            <div class="card-image">
              <figure class="image is-4by3">
                <v-lazy-image
                  :src="collection.image.src"
                  :src-placeholder="collection.image.placeholder"
                  :alt="collection.image.altText || collection.title" />
              </figure>
            </div>
            <div class="card-content">
              <div class="media">
                <div class="media-content">
                  <p class="title has-text-centered is-4 is-family-secondary">
                    {{ collection.title }}
                  </p>
                </div>
              </div>

              <div class="field is-grouped is-grouped-centered">
                <div class="control">
                  <g-link
                    :to="collection.path"
                    class="button is-white-ter">
                    Browse
                  </g-link>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script>
export default {
  computed: {
    collections () { return this.$page.allShopifyCollection.edges }
  }
}
</script>

<page-query>
query ShopifyProducts {
  allShopifyCollection (limit: 100) {
    edges {
      node {
        id
        path
        title
        descriptionHtml
        image {
          altText
          src: transformedSrc(maxWidth: 400, maxHeight: 300, crop: CENTER)
          placeholder: transformedSrc(maxWidth: 100, maxHeight: 75, crop: CENTER)
        }
      }
    }
  }
}
</page-query>

<style lang="scss" scoped>
.card {
  box-shadow: unset !important;
}
</style>
