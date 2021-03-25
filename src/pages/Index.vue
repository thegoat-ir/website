<template>
  <Layout :show-logo="false">
    <!-- Author intro -->
    <Author :show-title="true" />

    <!-- List posts -->
    <div class="posts">
      <PostCard
        v-for="edge in $page.posts.edges"
        :key="edge.node.id"
        :post="edge.node"
      />
    </div>
    <div class="repositories">
      <div v-if="errored"></div>
      <div v-else-if="loading">
        <div class="repository">
          <content-placeholders :rounded="true">
            <h4><content-placeholders-heading /></h4>
            <p><content-placeholders-text :lines="1" /></p>
            <div class="stars">
              <Star />
              <span class="star-count">0</span>
            </div>
          </content-placeholders>
        </div>
        <div class="repository">
          <content-placeholders :rounded="true">
            <h4><content-placeholders-heading /></h4>
            <p><content-placeholders-text :lines="1" /></p>
            <div class="stars">
              <Star />
              <span class="star-count">0</span>
            </div>
          </content-placeholders>
        </div>
        <div class="repository">
          <content-placeholders :rounded="true">
            <h4><content-placeholders-heading /></h4>
            <p><content-placeholders-text :lines="1" /></p>
            <div class="stars">
              <Star />
              <span class="star-count">0</span>
            </div>
          </content-placeholders>
        </div>
        <div class="repository">
          <content-placeholders :rounded="true">
            <h4><content-placeholders-heading /></h4>
            <p><content-placeholders-text :lines="1" /></p>
            <div class="stars">
              <Star />
              <span class="star-count">0</span>
            </div>
          </content-placeholders>
        </div>
      </div>
      <div v-else>
        <Repository
          v-for="repository in repositories"
          :key="repository.id"
          :url="repository.html_url"
          :title="repository.full_name"
          :description="repository.description"
          :starCount="repository.stargazers_count"
        />
      </div>
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
        date (format: "D. MMMM YYYY")
        timeToRead
        description
        cover_image (width: 770, height: 380, blur: 10)
        path
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
import Author from "~/components/Author.vue";
import PostCard from "~/components/PostCard.vue";
import Star from "~/components/Star.vue";
import Repository from "~/components/Repository.vue";
import axios from "axios";
export default {
  components: {
    Author,
    PostCard,
    Repository,
    Star,
  },
  data() {
    return {
      repositories: null,
      loading: true,
      errored: false,
    };
  },
  created() {
    axios
      .get(
        "https://api.github.com/orgs/thegoat-ir/repos?type=public&sort=updated&per_page=10&page=1"
      )
      .then((response) => (this.repositories = response.data))
      .catch((error) => {
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  metaInfo: {
    title: "The greatest of all time",
  },
};
</script>
<style lang="scss" scoped>
.repositories {
  width: 90%;
  margin: 20px auto;
  overflow: auto;
  white-space: nowrap;
  padding: 20px 10px;
}
.repositories::-webkit-scrollbar {
  height: .4em;
}

.repositories::-webkit-scrollbar-thumb {
  background-color: var(--scrollbar-color);
  border-radius: 16px;
  border: 4px solid var(--scrollbar-color);
}
.repositories::-webkit-scrollbar-button {
    display:none;
}
</style>
