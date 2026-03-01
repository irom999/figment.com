<script lang="ts">
	import { resolve } from '$app/paths';
	import { page } from '$app/state';
</script>

{#snippet underline(isPath: boolean, transparentDefault = false)}
	<span
		class={{
			'bg-accent-100': isPath,
			'bg-transparent': !isPath || transparentDefault,
		}}
		absolute
		h-0.5
		w-full
	></span>
{/snippet}

<header
	fcol
	fyc
	gap-y-lg
	grid
	grid-cols="1 md:3"
	mxa
	op="card hover:100"
	py-6
	text-xl
	transition-base
	view-transition--nav
>
	<div flex>
		{#if page.url.pathname === '/about'}
			<a aria-label="Back" href={resolve('/')} class="back-btn">
				<span class="arrow">←</span>
			</a>
		{:else}
			<a aria-label="Home" font-bold href={resolve('/')} m="xa md:(b0 x0)" relative>
				<div style:view-transition-name="title-irom999" class={{ hidden: page.url.pathname === '/' }}>
					@irom999
				</div>
				<div>{@render underline(page.url.pathname === '/', true)}</div>
			</a>
		{/if}
	</div>
	<nav col-span-2 flex="wrap" font-bold fyc gap-4 m="xa md:r0" md-fxe text-lg>
	</nav>
</header>

<style>
	a {
		--uno: no-underline;
	}

	.back-btn {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 2.2rem;
		height: 2.2rem;
		border-radius: 50%;
		border: 1.5px solid currentColor;
		opacity: 0.5;
		transition:
			opacity 0.2s ease,
			background-color 0.2s ease,
			color 0.2s ease;
	}

	.back-btn:hover {
		opacity: 1;
		background-color: currentColor;
	}

	.back-btn:hover .arrow {
		color: #FFFFD6;
		transform: translateX(-2px);
	}

	.arrow {
		font-size: 1rem;
		transition: transform 0.2s ease;
		display: block;
	}
</style>
