<script lang="ts">
	import Profile from '$components/Profile.svelte';
	import Social from '$components/Social.svelte';
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';

	let hasVisited = browser && sessionStorage.getItem('hasVisitedHome') === 'true';

	if (browser && !hasVisited) {
		sessionStorage.setItem('hasVisitedHome', 'true');
	}

	let bounceContainer: HTMLDivElement;
	let profileEls: HTMLDivElement[] = [];

	onMount(() => {
		if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;

		const bouncers = [
			{ x: 0, y: 0, vx: 2.5, vy: 2 },
			{ x: 0, y: 0, vx: -2, vy: 2.5 },
			{ x: 0, y: 0, vx: 1.5, vy: -1.8 },
		];
		let animId: number;

		// scale(1.1) expands from center → 5% overflow on each side
		const HOVER_MARGIN = 1.1 / 2 - 0.5; // 0.05

		const startBounce = () => {
			const cW = bounceContainer.clientWidth;
			const cH = bounceContainer.clientHeight;

			for (let i = 0; i < bouncers.length; i++) {
				const eW = profileEls[i].offsetWidth;
				const eH = profileEls[i].offsetHeight;
				const minX = eW * HOVER_MARGIN;
				const minY = eH * HOVER_MARGIN;
				bouncers[i].x = minX + Math.random() * (cW - eW * (1 + HOVER_MARGIN * 2));
				bouncers[i].y = minY + Math.random() * (cH - eH * (1 + HOVER_MARGIN * 2));
			}

			const animate = () => {
				const cW = bounceContainer.clientWidth;
				const cH = bounceContainer.clientHeight;

				for (let i = 0; i < bouncers.length; i++) {
					const el = profileEls[i];
					const b = bouncers[i];
					const eW = el.offsetWidth;
					const eH = el.offsetHeight;
					const minX = eW * HOVER_MARGIN;
					const maxX = cW - eW * (1 + HOVER_MARGIN);
					const minY = eH * HOVER_MARGIN;
					const maxY = cH - eH * (1 + HOVER_MARGIN);

					b.x += b.vx;
					b.y += b.vy;

					if (b.x <= minX) {
						b.x = minX;
						b.vx = Math.abs(b.vx);
					} else if (b.x >= maxX) {
						b.x = maxX;
						b.vx = -Math.abs(b.vx);
					}
					if (b.y <= minY) {
						b.y = minY;
						b.vy = Math.abs(b.vy);
					} else if (b.y >= maxY) {
						b.y = maxY;
						b.vy = -Math.abs(b.vy);
					}

					el.style.transform = `translate(${b.x}px, ${b.y}px)`;
				}

				animId = requestAnimationFrame(animate);
			};

			animId = requestAnimationFrame(animate);
		};

		const delay = hasVisited ? 0 : 1200;
		const timer = setTimeout(startBounce, delay);

		return () => {
			clearTimeout(timer);
			cancelAnimationFrame(animId);
		};
	});
</script>

<article container mt8 mxa fcol items-center>
	<!-- Marquee -->
	<div class="marquee-wrapper">
		<div class="marquee-track">
			<span class="marquee-text"
				>welcome to figment &nbsp;·&nbsp; figment🥚artwork &nbsp;·&nbsp; space☘️whimsical🙃
				&nbsp;·&nbsp;</span
			>
			<span class="marquee-text" aria-hidden="true"
				>welcome to figment &nbsp;·&nbsp; figment🥚artwork &nbsp;·&nbsp; space☘️whimsical🙃
				&nbsp;·&nbsp;</span
			>
			<span class="marquee-text" aria-hidden="true"
				>welcome to figment &nbsp;·&nbsp; figment🥚artwork &nbsp;·&nbsp; space☘️whimsical🙃
				&nbsp;·&nbsp;</span
			>
		</div>
	</div>

	<div
		bind:this={bounceContainer}
		class="relative w-full overflow-hidden"
		style="height: 45vh; min-height: 220px;"
	>
		<div
			bind:this={profileEls[0]}
			class="absolute"
			animate={hasVisited ? '' : 'duration-1000 keyframes-flip-in-x'}
		>
			<Profile label="About" />
		</div>
		<div bind:this={profileEls[1]} class="absolute">
			<Profile showTransition={false} grayscale={false} label="Contact" href="#" />
		</div>
		<div bind:this={profileEls[2]} class="absolute">
			<Profile showTransition={false} label="Pieces" href="#" />
		</div>
	</div>
</article>

<style>
	.word {
		display: inline-block;
		overflow: hidden;
		max-width: 0;
		animation: typing 0.3s steps(10) forwards;
		margin-right: 0;
		white-space: nowrap;
		opacity: 0;
	}

	a.word {
		color: #fb923c;
		text-decoration: underline;
		cursor: pointer;
		animation:
			typing 0.3s steps(10) forwards,
			color-change 3s ease-in-out infinite 1.4s;
	}

	a.word:hover {
		animation-play-state: paused;
	}

	.word-animation .word:nth-child(1) {
		animation-delay: 0.2s;
	}
	.word-animation .word:nth-child(2) {
		animation-delay: 0.5s;
	}
	.word-animation .word:nth-child(3) {
		animation-delay: 0.8s;
	}
	.word-animation .word:nth-child(4) {
		animation-delay: 1.1s;
	}
	.word-animation .word:nth-child(5) {
		animation-delay: 1.4s;
	}
	.word-animation .word:nth-child(6) {
		animation-delay: 1.7s;
	}
	.word-animation .word:nth-child(7) {
		animation-delay: 2s;
	}
	.word-animation .word:nth-child(8) {
		animation-delay: 2.5s;
	}
	.word-animation .word:nth-child(9) {
		animation-delay: 2.8s;
	}
	.word-animation .word:nth-child(10) {
		animation-delay: 3.1s;
	}
	.word-animation .word:nth-child(11) {
		animation-delay: 3.4s;
	}
	.word-animation .word:nth-child(12) {
		animation-delay: 3.9s;
	}
	.word-animation .word:nth-child(13) {
		animation-delay: 4.2s;
	}
	.word-animation .word:nth-child(14) {
		animation-delay: 4.5s;
	}
	.word-animation .word:nth-child(15) {
		animation-delay: 4.8s;
	}
	.word-animation .word:nth-child(16) {
		animation-delay: 5.1s;
	}
	.word-animation .word:nth-child(17) {
		animation-delay: 5.4s;
	}
	.word-animation .word:nth-child(18) {
		animation-delay: 5.7s;
	}
	.word-animation .word:nth-child(19) {
		animation-delay: 6s;
	}

	@keyframes typing {
		from {
			max-width: 0;
			opacity: 1;
		}
		to {
			max-width: 100%;
			opacity: 1;
		}
	}

	@keyframes color-change {
		0%,
		100% {
			color: #fb923c;
		}
		33% {
			color: #f97316;
		}
		66% {
			color: #c2410c;
		}
	}

.marquee-wrapper {
		align-self: flex-start;
		width: 100vw;
		margin-left: calc(50% - 50vw);
		overflow: hidden;
		margin-bottom: 1rem;
	}

	.marquee-track {
		display: flex;
		width: max-content;
		animation: marquee 15s linear infinite;
	}

	.marquee-text {
		white-space: nowrap;
		flex-shrink: 0;
		color: #22c55e;
		font-size: 1.25rem;
		font-weight: 100;
		font-family: Arial, sans-serif;
		letter-spacing: 0.05em;
	}

	@media (prefers-reduced-motion: reduce) {
		.marquee-track {
			animation: none;
		}
	}

	@keyframes marquee {
		from {
			transform: translateX(0);
		}
		to {
			transform: translateX(-33.333%);
		}
	}
</style>
