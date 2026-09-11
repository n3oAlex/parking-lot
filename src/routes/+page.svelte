<script lang="ts">
	import { onMount } from 'svelte';

	const QUIPS = [
		'Lot attendant on break.',
		'Your subdomain could be here.',
		'404: car not found.',
		'Free parking. No validation required.'
	];

	// Both are filled in on the client: the same prerendered HTML is served from
	// every hostname, so neither value can be baked in at build time.
	let host = $state('this domain');
	let quip = $state(QUIPS[0]);

	onMount(() => {
		host = window.location.hostname;
		quip = QUIPS[Math.floor(Math.random() * QUIPS.length)];
	});
</script>

<svelte:head>
	<title>Empty lot</title>
	<meta name="robots" content="noindex" />
</svelte:head>

<main>
	<div class="lot" aria-hidden="true">
		<span class="stripe"></span>
		<span class="stripe"></span>
		<span class="stripe"></span>
		<span class="stripe"></span>
	</div>

	<p class="code">404</p>
	<h1>Nobody parked anything at <span class="host">{host}</span> yet.</h1>
	<p class="quip">{quip}</p>
	<p class="owner">This domain belongs to Alex Hanák and is reserved for a future project.</p>
</main>

<style>
	:global(html) {
		--bg: #fafaf9;
		--fg: #1c1917;
		--muted: #78716c;
		--line: #d6d3d1;
		--mono: ui-monospace, 'SF Mono', Menlo, Consolas, monospace;
		color-scheme: light;
	}

	@media (prefers-color-scheme: dark) {
		:global(html) {
			--bg: #0c0a09;
			--fg: #f5f5f4;
			--muted: #a8a29e;
			--line: #292524;
			color-scheme: dark;
		}
	}

	:global(body) {
		margin: 0;
		background: var(--bg);
		color: var(--fg);
		font: 16px/1.6 ui-sans-serif, system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
	}

	main {
		box-sizing: border-box;
		min-height: 100dvh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 0.75rem;
		max-width: 34rem;
		margin-inline: auto;
		padding: 2rem 1.5rem 3rem;
	}

	.lot {
		display: flex;
		width: fit-content;
		gap: 3.5rem;
		height: 4.5rem;
		margin-bottom: 1.5rem;
		border-bottom: 3px solid var(--line);
	}

	.stripe {
		width: 3px;
		background: var(--line);
	}

	.code {
		margin: 0;
		font: 0.8rem/1 var(--mono);
		letter-spacing: 0.24em;
		color: var(--muted);
	}

	h1 {
		margin: 0;
		font-size: clamp(1.6rem, 5vw, 2.3rem);
		font-weight: 600;
		line-height: 1.25;
		letter-spacing: -0.02em;
		text-wrap: balance;
	}

	.host {
		font-family: var(--mono);
		font-size: 0.85em;
		word-break: break-all;
		border-bottom: 2px solid var(--line);
	}

	.quip {
		margin: 0;
		font-size: 1.05rem;
		color: var(--muted);
	}

	.owner {
		margin: 1.5rem 0 0;
		padding-top: 1.25rem;
		border-top: 1px solid var(--line);
		font-size: 0.875rem;
		color: var(--muted);
	}
</style>
