<script>
	import File from './File.svelte';
	import Folder from './Folder.svelte';
	import { slide } from 'svelte/transition';

	let { expanded = $bindable(false), name, files } = $props();

	function toggle() {
		expanded = !expanded;
	}
</script>

<button class:expanded onclick={toggle}>{name}</button>

{#if expanded}
	<ul transition:slide={{ duration: 300 }}>
		{#each files as file}
			<li>
				{#if file.type === 'folder'}
					<Folder {...file} />
				{:else}
					<File {...file} />
				{/if}
			</li>
		{/each}
	</ul>
{/if}

<style>
	button {
		padding: 0 0 0 1.5em;
		background: url(/tutorial/icons/folder.svg) 0 0.1em no-repeat;
		background-size: 1em 1em;
		font-weight: bold;
		cursor: pointer;
		border: none;
		font-size: 14px;
	}

	.expanded {
		background-image: url(/tutorial/icons/folder-open.svg);
	}

	ul {
		padding: 0.2em 0 0 0.5em;
		margin: 0 0 0 0.5em;
		list-style: none;
		border-left: 1px solid #eee;
	}

	li {
		padding: 0.2em 0;
	}
</style>
