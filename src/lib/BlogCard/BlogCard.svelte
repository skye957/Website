<script lang="ts">
	import { externalLink } from "$lib";
	import { InfoBadge } from "fluent-svelte";
	import { date as dateFormat } from "svelte-i18n";

	export let slug = "";
	export let date = "";
	export let author = "";
	export let title = "";
	export let description = "";
	export let thumbnail = "";
	export let tags: string[] = [];
</script>

<a class="blog-card" href="/blog/posts/{slug}" {...$$restProps}>
	<img alt="{title} thumbnail" class="thumbnail" src={thumbnail} />
	<div class="body">
		<h5>{title}</h5>
		{#if tags.length > 0}
			<ul class="blog-card-tag-list">
				{#each tags as tag}
					<li class="blog-card-tag">
						<InfoBadge>{tag}</InfoBadge>
					</li>
				{/each}
			</ul>
		{/if}
		<span>{description}</span>
	</div>
	<footer>
		<img
			alt="{author} avatar"
			loading="lazy"
			src="https://github.com/{author}.png"
		/>
		<div class="post-info">
			<object aria-label="Author link">
				<a href="https://github.com/{author}" {...externalLink}>
					{author}
				</a>
			</object>
			<span>{$dateFormat(new Date(date), { format: "medium" })}</span>
		</div>
	</footer>
	<slot />
</a>

<style lang="scss">
	@use "./BlogCard";
</style>
