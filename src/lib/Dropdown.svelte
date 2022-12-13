<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	/**
	 * Variables
	 */

	export var position = 'is-bottom-right';
	export var separated: boolean = false;
	export var onOpen: () => void = () => {};
	export var onClose: () => void = () => {};

	// is_visible
	var is_visible: boolean = false;
	// self
	var self: HTMLElement = null;
	// toggler
	var toggler: HTMLElement = null;

	/**
	 * System
	 */

	onMount(() => {
		document.addEventListener('click', hide);
	});

	onDestroy(() => {
		document.removeEventListener('click', hide);
	});

	/**
	 * Methods
	 */

	// show
	export function show() {
		is_visible = true;
		if (is_visible) {
			onOpen();
		} else {
			onClose();
		}
	}

	// hide
	export function hide(e: MouseEvent) {
		if ((e.target as HTMLElement) === toggler) {
			return;
		}
		if (self.contains(e.target as HTMLElement)) {
			setTimeout(() => {
				is_visible = false;
				if (is_visible) {
					onOpen();
				} else {
					onClose();
				}
			}, 1);
			return;
		}
		is_visible = false;
		if (is_visible) {
			onOpen();
		} else {
			onClose();
		}
	}

	// toggle
	export function toggle(e: MouseEvent) {
		toggler = e.target as HTMLElement;
		is_visible = !is_visible;

		if (is_visible) {
			onOpen();
		} else {
			onClose();
		}
	}
</script>

<div
	class={`ts-dropdown is-start-icon is-${position}`}
	class:is-separated={separated}
	class:is-visible={is_visible}
	bind:this={self}
>
	<slot />
</div>
