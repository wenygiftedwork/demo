<script lang="ts">
	import { writable, derived } from 'svelte/store';
	import CounterGroup from './CounterGroup.svelte';
	
	interface CounterGroup {
	  	id: number;
	  	count: number;
	  	title: string;
	}
	
	const counterGroups = writable<CounterGroup[]>([
  		{ id: 0, count: 0, title: 'new' }
	]);

	let nextId = 1;
  
	const addGroup = (): void => {
	  	counterGroups.update(currentGroups => 
			[...currentGroups, { id: nextId++, count: 0, title: 'new' }]
	  	);
	}
  
	const removeGroup = (id: number): void => {
	  	counterGroups.update(currentGroups => 
			currentGroups.filter(group => group.id !== id)
	  	);
	}
  
	const totalCounts = derived(counterGroups, $counterGroups => 
	  	$counterGroups.reduce((sum, group) => sum + group.count, 0)
	);
	
	$: allGroupTitles = $counterGroups.map(group => group.title).join(', '); 
  </script>
  
 <main>
	<div class="content_wrap text-center">
		<h1>Multiple Counter</h1>
		{#each $counterGroups as group (group.id)}
		<CounterGroup 
		bind:count={group.count} 
		bind:title={group.title}
		on:remove={() => removeGroup(group.id)}
		/>
		{/each}
		<button class="btn btn-sm btn-success new_btn" on:click={addGroup}>new counter</button>
	
		<p class="title">title list: {allGroupTitles}</p>
		<p>sum  of count: {$totalCounts}</p>
	</div>
</main> 
