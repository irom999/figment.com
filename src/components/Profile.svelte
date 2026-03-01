<script lang="ts">
	let { showTransition = true }: { showTransition?: boolean } = $props();
</script>

<div>
	<a href="/bio">
		<img
			class="mx-auto aspect-square w-1/2 rounded-full object-cover md:size-64 hover:scale-110 hover:grayscale-0 transition-all duration-300 cursor-pointer"
			style:view-transition-name={showTransition ? 'profile' : undefined}
			alt="profile"
			fetchpriority="high"
			loading="eager"
			src="/my_pic.JPG"
			grayscale
		/>
	</a>
</div>
