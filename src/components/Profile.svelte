<script lang="ts">
	let {
		showTransition = true,
		grayscale = true,
		label = '',
		href = '/about',
	}: {
		showTransition?: boolean;
		grayscale?: boolean;
		label?: string;
		href?: string;
	} = $props();
</script>

<a {href} class={['profile-anchor', grayscale ? 'starts-gray' : 'starts-color']}>
	<img
		class="profile-img aspect-square size-20 md:size-52 rounded-full object-cover cursor-pointer"
		style:view-transition-name={showTransition ? 'profile' : undefined}
		alt="profile"
		fetchpriority="high"
		loading="eager"
		src="/my_pic.JPG"
	/>
	{#if label}
		<div class="label-overlay" aria-hidden="true">
			<span class="label-text">{label}</span>
		</div>
	{/if}
</a>

<style>
	.profile-anchor {
		display: inline-block;
		position: relative;
	}

	.profile-img {
		transition:
			transform 0.3s ease,
			filter 0.3s ease;
	}

	.starts-gray .profile-img {
		filter: grayscale(1);
	}

	.starts-gray:hover .profile-img {
		transform: scale(1.1);
		filter: grayscale(0);
	}

	.starts-color:hover .profile-img {
		transform: scale(1.1);
		filter: grayscale(1);
	}

	.label-overlay {
		position: absolute;
		inset: 0;
		border-radius: 50%;
		background: rgba(0, 0, 0, 0.45);
		display: flex;
		align-items: center;
		justify-content: center;
		opacity: 0;
		transition: opacity 0.25s ease;
		pointer-events: none;
	}

	.profile-anchor:hover .label-overlay {
		opacity: 1;
	}

	.label-text {
		color: rgba(255, 255, 255, 0.4);
		font-size: 0.9rem;
		font-weight: 100;
		letter-spacing: 0.1em;
		text-transform: uppercase;
	}

	@media (prefers-reduced-motion: reduce) {
		.profile-img,
		.label-overlay {
			transition: none;
		}
	}
</style>
