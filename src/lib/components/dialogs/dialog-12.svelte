<script lang="ts">
	import Button, { buttonVariants } from '$lib/components/ui/button.svelte';
	import * as Dialog from '$lib/components/ui/dialog/index.js';
	import * as InputOTP from '$lib/components/ui/input-otp/index.js';

	import { cn } from '$lib/utils';

	const CORRECT_CODE = '6548';

	let myValue = $state('');
	let hasGuessed: boolean | undefined = $state(undefined);
	let inputRef = $state<HTMLInputElement | null>(null);
	let closeButtonRef = $state<HTMLButtonElement | null>(null);

	$effect(() => {
		if (hasGuessed) {
			closeButtonRef?.focus();
		}
	});

	function processCode() {
		hasGuessed = myValue === CORRECT_CODE;
		myValue = '';
		setTimeout(() => {
			inputRef?.blur();
		}, 20);
	}

</script>

<Dialog.Root>
	<Dialog.Trigger class={buttonVariants({ variant: 'outline' })}>OTP code</Dialog.Trigger>
	<Dialog.Content>
		<div class="flex flex-col items-center gap-2">
			<div aria-hidden="true" class="flex size-11 shrink-0 items-center justify-center rounded-full border">
				<svg
					aria-hidden="true"
					class="stroke-zinc-800 dark:stroke-zinc-100"
					height="20"
					viewBox="0 0 32 32"
					width="20"
					xmlns="http://www.w3.org/2000/svg"
				>
					<circle cx="16" cy="16" fill="none" r="12" stroke-width="8" />
				</svg>
			</div>
			<Dialog.Header>
				<Dialog.Title class="sm:text-center">
					{hasGuessed ? "Code verified!" : "Enter confirmation code"}
				</Dialog.Title>
				<Dialog.Description class="sm:text-center">
					{hasGuessed
						? "Your code has been successfully verified."
						: `Check your email and enter the code - Try ${CORRECT_CODE}`}
				</Dialog.Description>
			</Dialog.Header>
		</div>

		{#if hasGuessed}
			<div class="text-center">
				<Dialog.Close>
					<Button type="button" bind:ref={closeButtonRef}>
						Close
					</Button>
				</Dialog.Close>
			</div>
		{:else}
			<div class="space-y-4">
				<div class="flex justify-center">
					<InputOTP.Root id="confirmation-code"
												 bind:ref={inputRef}
												 bind:value={myValue}
												 onComplete={() => (processCode())}
												 onfocus={() => (hasGuessed = undefined)}
												 maxlength={4}
												 class="flex items-center gap-3 has-disabled:opacity-50"
					>
						{#snippet children({ cells })}
							<InputOTP.Group class="flex gap-2">
								{#each cells as cell, index (index)}
									<InputOTP.Slot {cell} class={cn(
										"border-input bg-background text-foreground flex size-9 items-center justify-center rounded-md border font-medium shadow-xs transition-[color,box-shadow]",
										{ "border-ring ring-ring/50 z-10 ring-[3px]": onfocus }
									)} />
								{/each}
							</InputOTP.Group>
						{/snippet}
					</InputOTP.Root>
				</div>
				{#if hasGuessed === false}
					<p
						class="text-muted-foreground text-center text-xs"
						role="alert"
						aria-live="polite"
					>
						Invalid code. Please try again.
					</p>
				{/if}
				<p class="text-center text-sm">
					<a class="underline hover:no-underline" href="#">
						Resend code
					</a>
				</p>
			</div>
		{/if}
	</Dialog.Content>
</Dialog.Root>