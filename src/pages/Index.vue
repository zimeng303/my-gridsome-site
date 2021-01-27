<template>
  <Layout>
    <!-- Page Header -->
    <header 
      class="masthead" 
      :style="{backgroundImage: `url(${GRIDSOME_API_URL + general.cover.url})`}">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/posts/' + edge.node.id">
              <h2 class="post-title">
               {{ edge.node.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <p class="post-meta">
              Posted by
              <g-link to="/">Start Bootstrap</g-link>
              on {{ edge.node.create_at }}
            </p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
              <g-link :to="'/tags/' + tag.id">
                {{ tag.title }}
                </g-link>
              </span>
            </p>

            <hr />
          </div>

          <!-- Pager -->
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right" href="#"
              >Older Posts &rarr;</a>
          </div> -->
          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPosts (perPage: 1, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
  	edges {
      node {
        id
        title  
        created_at
        tags {
          id
          title
        }
			} 
    }
	}

  allStrapiGeneral {
    edges {
      node {
        id
        title
        subtitle
        cover {
          url
        }
      }
    }
  }
}
</page-query>

<script>

// 引入分页组件
import { Pager } from 'gridsome'

export default {
  name: "HomePage",
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager
  },
  computed: {
    general () {
      return this.$page.allStrapiGeneral.edges[0].node
    }
  }
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
