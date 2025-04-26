<script lang="ts">
	import type { ComponentProps } from 'svelte';

	import { cn } from '$lib/utils.js';

	import { PinInput as InputOTPPrimitive } from 'bits-ui';

	let {
		cell,
		class: className,
		ref = $bindable(null),
		...restProps
	}: ComponentProps<typeof InputOTPPrimitive.Cell> = $props();
</script>

<InputOTPPrimitive.Cell
	{...restProps}
	bind:ref
	{cell}
	class={cn(
		"border-input relative flex h-9 w-9 items-center justify-center border-y border-r text-sm shadow-sm transition-all first:rounded-l-md first:border-l last:rounded-r-md",
		cell.isActive && "ring-ring z-10 ring-1",
		className
	)}
>
	{cell.char}
	{#if cell.hasFakeCaret}
		<div class="pointer-events-none absolute inset-0 flex items-center justify-center">
			<div class="animate-caret-blink bg-foreground h-4 w-px duration-1000"></div>
		</div>
	{/if}
</InputOTPPrimitive.Cell>