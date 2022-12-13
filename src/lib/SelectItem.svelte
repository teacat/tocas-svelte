<script lang="ts">
	/**
	 * Variables
	 */

	export var content: string = '';
	export var onClick: () => void = () => {};
</script>

<button class="item" on:click={onClick}>
	{@html content}
</button>
