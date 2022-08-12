<template>
	<Layout>
		<!-- Page Header-->
		<header
			class="masthead"
			:style="{
				backgroundImage: `url(${GridsomeApiUrl +
					$page.about.edges[0].node.cover.url})`,
			}"
		>
			<div class="container position-relative px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div class="col-md-10 col-lg-8 col-xl-7">
						<div class="page-heading">
							<h1>{{ $page.about.edges[0].node.name }}</h1>
							<!-- <span class="subheading">{{
								$page.about.edges[0].node.description
							}}</span> -->
						</div>
					</div>
				</div>
			</div>
		</header>
		<!-- Main Content-->
		<main class="mb-4">
			<div class="container px-4 px-lg-5">
				<div class="row gx-4 gx-lg-5 justify-content-center">
					<div
						class="col-md-10 col-lg-8 col-xl-7"
						v-html="markdownToHtml($page.about.edges[0].node.description)"
					></div>
				</div>
			</div>
		</main>
	</Layout>
</template>
<page-query>
query {
  about: allStrapiAbout {
    edges {
      node {
        id
        name
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
import MarkdownIt from 'markdown-it';
const md = new MarkdownIt();
export default {
	metaInfo: {
		title: 'About us',
	},
	methods: {
		markdownToHtml(markdownString) {
			return md.render(markdownString);
		},
	},
};
</script>
