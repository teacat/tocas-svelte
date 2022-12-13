<script lang="ts">
	/**
	 * Variables
	 */

	export var title: string = '';
	export var size: string = '';
	var is_visible: boolean = false;

	/**
	 * Methods
	 */

	// show
	export function show() {
		is_visible = true;
	}

	// hide
	export function hide() {
		is_visible = false;
	}

	// hideClick
	function hideClick(e: MouseEvent) {
		if (
			(e.target as HTMLElement).tagName === 'T-MODAL' ||
			(e.target as HTMLElement).tagName === 'T-CLOSE'
		) {
			is_visible = false;
		}
	}
</script>

<t-modal
	class="ts-modal"
	class:is-large={size === 'large'}
	class:is-visible={is_visible}
	on:click={hideClick}
	on:keydown={hideClick}
>
	<div class="content" style="overflow: visible">
		<div class="ts-content is-horizontally-padded">
			<div class="ts-row">
				<div class="column is-fluid">
					<div class="ts-header">{title}</div>
				</div>
				<div class="column">
					<t-close class="ts-close is-secondary is-big is-rounded" on:click={hideClick} />
				</div>
			</div>
		</div>
		<div class="ts-divider" />
		<slot />
	</div>
</t-modal>
