<template>
	<Layout>
		<!-- Page Header-->
		<header
			class="masthead"
			:style="{
				backgroundImage: `url(${GridsomeApiUrl + abstract.cover.url})`,
			}"
		>
			<div class="container position-relative px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div class="col-md-10 col-lg-8 col-xl-7">
						<div class="site-heading">
							<h1>{{ abstract.title }}</h1>
							<span class="subheading">{{ abstract.description }}</span>
						</div>
					</div>
				</div>
			</div>
		</header>
		<!-- Main Content-->
		<div class="container px-4 px-lg-5">
			<div class="row gx-4 gx-lg-5 justify-content-center">
				<div class="col-md-10 col-lg-8 col-xl-7">
					<template v-for="post in $page.allStrapiPost.edges">
						<div :key="post.node.id">
							<!-- Post preview-->
							<div class="post-preview">
								<g-link :to="`post/${post.node.id}`">
									<h2 class="post-title">
										{{ post.node.title }}
									</h2>
									<h3 class="post-subtitle">
										{{ post.node.subtitle }}
									</h3>
								</g-link>
								<div class="post-meta">
									<p>
										Posted by
										<a href="#!">{{ post.node.author.name }}</a>
										{{ post.node.created_at }}
									</p>
									<p>
										<span v-for="tag in post.node.tags" :key="tag.id">
											<g-link :to="`/tag/${tag.id}`">{{ tag.title }}</g-link
											>&nbsp;&nbsp;
										</span>
									</p>
								</div>
							</div>
							<!-- Divider-->
							<hr class="my-4" />
						</div>
					</template>

					<!-- Pager-->
					<div class="d-flex justify-content-end mb-4">
						<!-- <a class="btn btn-primary text-uppercase" href="#!"
							>Older Posts →</a
						> -->
						<Pager :info="$page.allStrapiPost.pageInfo" />
					</div>
				</div>
			</div>
		</div>
	</Layout>
</template>

<page-query>
query($page:Int) {
  allStrapiPost(perPage: 2, page: $page) @paginate {
	pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        subtitle
        author {
          id
          name
        }
        tags {
			id
          title
        }
        content
        created_at
      }
    }
  }
  allStrapiAbstract {
    edges {
      node {
        id
        title
        subtitle
        description
        cover {
          url
        }
      }
    }
  }
}
</page-query>
<script>
import { Pager } from 'gridsome';
export default {
	components: {
		Pager,
	},
	metaInfo: {
		title: 'Hello, world!',
	},
	computed: {
		abstract() {
			return this.$page.allStrapiAbstract.edges[0].node;
		},
	},
};
</script>
