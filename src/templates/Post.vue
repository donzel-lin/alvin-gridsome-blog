<template>
	<Layout>
		<!-- Page Header-->
		<header
			class="masthead"
			:style="{
				backgroundImage: `url(${GridsomeApiUrl + $page.post.cover.url})`,
			}"
		>
			<div class="container position-relative px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div class="col-md-10 col-lg-8 col-xl-7">
						<div class="post-heading">
							<h1>{{ $page.post.title }}</h1>
							<h2 class="subheading">
								{{ $page.post.subtitle }}
							</h2>
							<!-- <span class="meta">
								Posted by
								<a href="#!">{{ $page.post.author.name }}</a>
								on {{ $page.post.created_at }}
							</span> -->
							<div class="meta">
								<p>
									Posted by
									<a href="#!">{{ $page.post.author.name }}</a>
									{{ $page.post.created_at }}
								</p>
								<p>
									<span v-for="tag in $page.post.tags" :key="tag.id">
										<g-link :to="`/tag/${tag.id}`">{{ tag.title }}</g-link
										>&nbsp;&nbsp;
									</span>
								</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</header>
		<!-- Post Content-->
		<article class="mb-4">
			<div class="container px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div
						class="col-md-10 col-lg-8 col-xl-7"
						v-html="markdownToHtml($page.post.content)"
					></div>
				</div>
			</div>
		</article>
	</Layout>
</template>
<page-query>
query($id:ID!) {
	post:strapiPost(id:$id) {
		id
		title
		subtitle
		content
		cover {
			url
		}
		author {
			id
			name
		}
		tags {
			title
			id
		}
		created_at
	}
}
</page-query>
<script>
import MarkdownIt from 'markdown-it';
const md = new MarkdownIt();
export default {
	name: 'Post',
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
