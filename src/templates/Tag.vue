<template>
	<Layout>
		<!-- Page Header-->
		<header class="masthead">
			<div class="container position-relative px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div class="col-md-10 col-lg-8 col-xl-7">
						<div class="post-heading">
							<h1>{{ $page.strapiTag.title }}</h1>
						</div>
					</div>
				</div>
			</div>
		</header>
		<!-- Post Content-->
		<div class="container px-4 px-lg-5">
			<div class="row gx-4 gx-lg-5 justify-content-center">
				<div class="col-md-10 col-lg-8 col-xl-7">
					<template v-for="post in $page.strapiTag.posts">
						<div :key="post.id">
							<!-- Post preview-->
							<div class="post-preview">
								<g-link :to="`post/${post.id}`">
									<h2 class="post-title">
										{{ post.title }}
									</h2>
									<h3 class="post-subtitle">
										{{ post.subtitle }}
									</h3>
								</g-link>
								<div class="post-meta">
									<p>
										Posted by
										<a href="#!">{{ post.author }}</a>
										{{ post.created_at }}
									</p>
								</div>
							</div>
							<!-- Divider-->
							<hr class="my-4" />
						</div>
					</template>
				</div>
			</div>
		</div>
	</Layout>
</template>
<page-query>
query($id:ID!) {
  strapiTag(id:$id) {
    id
    title
    posts {
      id
      content
      title
      subtitle
      author
      created_at
    }
  }
}
</page-query>
<script>
import MarkdownIt from 'markdown-it';
const md = new MarkdownIt();
export default {
	name: 'Tag',
	methods: {
		markdownToHtml(markdownString) {
			return md.render(markdownString);
		},
	},
	computed: {
		rootUrl() {
			return 'http://120.46.147.119:1337';
		},
	},
};
</script>
