<script lang="ts">
	import Button from '$lib/components/ui/button.svelte';

	import SquareArrowOutUpRight from 'lucide-svelte/icons/square-arrow-out-up-right';
</script>

<div class="inline-flex -space-x-px rounded-lg shadow-sm shadow-black/[0.04] rtl:space-x-reverse">
	<Button
		class="rounded-none shadow-none first:rounded-s-lg last:rounded-e-lg focus-visible:z-10"
		variant="outline"
	>
		Preview
	</Button>
	<Button
		class="rounded-none shadow-none first:rounded-s-lg last:rounded-e-lg focus-visible:z-10"
		variant="outline"
		size="icon"
		aria-label="Open link"
	>
		<SquareArrowOutUpRight size={16} stroke-width={2} aria-hidden="true" />
	</Button>
</div>
