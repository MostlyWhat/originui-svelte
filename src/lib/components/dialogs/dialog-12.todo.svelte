<script lang="ts">
	import { cn } from "$lib/utils"
	import Button, { buttonVariants } from '$lib/components/ui/button.svelte';
	import * as Dialog from '$lib/components/ui/dialog/index.js';
	import * as InputOTP from "$lib/components/ui/input-otp/index.js";

	const CORRECT_CODE = "6548"

	const [value, setValue] = $state("")
	const [hasGuessed, setHasGuessed] = $state(undefined)
	const inputRef = useRef<HTMLInputElement>(null)
	const closeButtonRef = useRef<HTMLButtonElement>(null)

	$effect(() => {
		if (hasGuessed) {
			closeButtonRef.current?.focus()
		}
	}, [hasGuessed])

	async function onSubmit(e?: React.FormEvent<HTMLFormElement>) {
		e?.preventDefault?.()

		inputRef.current?.select()
		await new Promise((r) => setTimeout(r, 1_00))

		setHasGuessed(value === CORRECT_CODE)

		setValue("")
		setTimeout(() => {
			inputRef.current?.blur()
		}, 20)
	}

	function Slot(props: SlotProps) {
		return (
			<div class=
			>
				{props.char !== null && <div>{props.char}</div>}
			</div>
			)
		}

</script>

<Dialog.Root>
	<Dialog.Trigger asChild>
		<Button variant="outline">OTP code</Button>
	</Dialog.Trigger>
	<Dialog.Content>
		<div class="flex flex-col items-center gap-2">
			<div
			class="flex size-11 shrink-0 items-center justify-center rounded-full border"
			aria-hidden="true"
			>
				<svg
				class="stroke-zinc-800 dark:stroke-zinc-100"
				xmlns="http://www.w3.org/2000/svg"
				width="20"
				height="20"
				viewBox="0 0 32 32"
				aria-hidden="true"
				>
				<circle cx="16" cy="16" r="12" fill="none" stroke-width="8" />
				</svg>
			</div>
			<Dialog.Header>
				<Dialog.Title class="sm:text-center">
					{hasGuessed ? "Code verified!" : "Enter confirmation code"}
				</Dialog.Title>
				<Dialog.Description class="sm:text-center">
					{hasGuessed ? "Your code has been successfully verified.": `Check your email and enter the code - Try ${CORRECT_CODE}`}
				</Dialog.Description>
			</Dialog.Header>
		</div>

		{#if hasGuessed}
			<div class="text-center">
				<Dialog.Close asChild>
					<Button type="button" ref={closeButtonRef}>
						Close
					</Button>
				</Dialog.Close>
			</div>
			) : (
			<div class="space-y-4">
				<div class="flex justify-center">
					<InputOTP.Root maxlength={4}>
						{#snippet children({ cells })}
							<InputOTP.Group>
								{#each cells.slice(0, 4) as cell}
									<InputOTP.Slot {cell} />
								{/each}
							</InputOTP.Group>
						{/snippet}
					</InputOTP.Root>
					<OTPInput.Root
						id="cofirmation-code"
						ref={inputRef}
						value={value}
						onChange={setValue}
						containerClassName="flex items-center gap-3 has-disabled:opacity-50"
						maxLength={4}
						onFocus={() => setHasGuessed(undefined)}
						render={({ slots }) => (
				<div class="flex gap-2">
				{slots.map((slot, idx) => (
				<Slot key={idx} {...slot} />
				))}
				</div>
				)}
						onComplete={onSubmit}
					/>
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