<script lang="ts">
	import Button from '$lib/components/ui/button.svelte';

	import ThumbsUp from 'lucide-svelte/icons/thumbs-up';
</script>

<Button class="py-0 pe-0" variant="outline">
	<ThumbsUp class="me-2 opacity-60" size={16} stroke-width={2} aria-hidden="true" />
	Like
	<span
		class="relative ms-3 inline-flex h-full items-center justify-center rounded-full px-3 text-xs font-medium text-muted-foreground before:absolute before:inset-0 before:left-0 before:w-px before:bg-input"
	>
		86
	</span>
</Button>
