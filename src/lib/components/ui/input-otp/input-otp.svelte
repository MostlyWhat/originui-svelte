<script lang="ts">
	import type { ComponentProps } from 'svelte';

	import { cn } from '$lib/utils.js';

	import { PinInput as InputOTPPrimitive } from 'bits-ui';

	let {
		class: className,
		ref = $bindable(null),
		value = $bindable(''),
		...restProps
	}: ComponentProps<typeof InputOTPPrimitive.Root> = $props();
</script>

<InputOTPPrimitive.Root
	{...restProps}
	bind:ref
	bind:value
	class={cn(
		"flex items-center gap-2 has-[:disabled]:opacity-50 [&_input]:disabled:cursor-not-allowed",
		className
	)}
/>