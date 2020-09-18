<template>
  <Layout :show-logo="false">
    <!-- Author intro -->
    <Author :show-title="true" />

	<!-- Tag list -->
	<div v-for="edge in $page.posts.edges" :key="edge.node.id">
		{{ edge.node.category }}
	</div>

    <!-- List posts -->
    <div class="posts">
      <PostCard v-for="edge in $page.posts.edges" :key="edge.node.id" :post="edge.node"/>
    </div>

  </Layout>
</template>

<page-query>
query {
  posts: allPost(filter: { published: { eq: true }}) {
    edges {
      node {
        id
        title
        date (format: "YYYY.MM.DD")
        timeToRead
        description
        cover_image (width: 770, height: 380, blur: 10)
        path
		category
        tags {
          id
          title
          path
        }
      }
    }
  }
}
</page-query>

<script>
import Author from '~/components/Author.vue'
import PostCard from '~/components/PostCard.vue'

export default {
  components: {
    Author,
    PostCard
  },
  metaInfo: {
    title: 'Hello, world!'
  }
}
</script>
