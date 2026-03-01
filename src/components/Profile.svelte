<script lang="ts">
	let { showTransition = true, grayscale = true }: { showTransition?: boolean; grayscale?: boolean } = $props();
</script>

<div>
	<a href="/bio">
		<img
			class={['mx-auto aspect-square w-1/3 rounded-full object-cover md:size-40 hover:scale-110 transition-all duration-300 cursor-pointer', grayscale ? 'grayscale hover:grayscale-0' : 'hover:grayscale']}
			style:view-transition-name={showTransition ? 'profile' : undefined}
			alt="profile"
			fetchpriority="high"
			loading="eager"
			src="/my_pic.JPG"
		/>
	</a>
</div>
