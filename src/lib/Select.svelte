<script lang="ts" context="module">
</script>

<script lang="ts">
	/** Components */
	import SelectItem from './SelectItem.svelte';
	import Dropdown from './Dropdown.svelte';

	/**
	 * Variables
	 */

	export var items: any[][] = [];
	export var value: any = '';
	export var onChange: (v: string) => void = (v: string) => {};

	var content: string = '&nbsp;';
	var dropdown: Dropdown;
	var is_active: boolean = false;

	$: content = items.find((v) => {
		return v[0] === value;
	})?.[1];

	/**
	 * Methods
	 */

	// onSelect
	function onSelect(v: string, c: string) {
		value = v;
		onChange(v);
	}
</script>

<div
	class="ts-select is-solid is-fluid"
	class:is-active={is_active}
	on:click={dropdown.toggle}
	on:keydown={dropdown.toggle}
>
	<div class="content">
		{@html content}
	</div>
	<Dropdown
		bind:this={dropdown}
		position="bottom"
		onOpen={() => {
			is_active = true;
		}}
		onClose={() => {
			is_active = false;
		}}
	>
		{#each items as item}
			<svelte:component
				this={SelectItem}
				value={item[0]}
				content={item[1]}
				onClick={() => {
					onSelect(item[0], item[1]);
				}}
			/>
		{/each}
	</Dropdown>
</div>
