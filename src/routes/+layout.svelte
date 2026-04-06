<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { onMount } from 'svelte';

	onMount(async () => {
		await import('bootstrap/dist/js/bootstrap.bundle.min.js');
		await import('bootstrap/dist/css/bootstrap.min.css');
	});

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
{@render children()}
