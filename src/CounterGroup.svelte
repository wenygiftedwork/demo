<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	export let count: number = 0;
	export let title: string = '';
  
	const dispatch = createEventDispatcher();
  
	const increment = (): void => {
		count += 1;
	}
  
	const decrement = (): void => {
	  	if (count > 0) count -= 1;
	}
  
	const reset = (): void => {
	  	count = 0;
	}
  </script>
  
 <main>

	<div class="btn-toolbar input-group">
		<div class="btn-group input-group-text">
			<input type="text" class="txt_input" bind:value={title} placeholder="new" />
			<span class="label label-default cnt_label">{count}</span>
			<button type="button" class="btn btn-danger l_radius" on:click={increment}>+</button>
			<button type="button" class="btn btn-primary" on:click={decrement}>-</button>
			<button type="button" class="btn btn-warning r_radius text-white" on:click={reset}>0</button>
			<button type="button" class="btn btn-default t_gray" on:click={() => dispatch('remove')}>x</button>
		</div>
	</div>

</main> 
