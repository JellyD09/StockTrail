<script lang="ts">
	import Button from './../ui/button/button.svelte';
	import Input from '../ui/input/input.svelte';
	import { supabase } from '#lib/SupabaseClient.js';

	let email = $state("");
	let password = $state("");
	let pesanEmail = $state("");
	let pesanPassword = $state("")
	let loading = $state(false);

	async function login(e: SubmitEvent) {
		e.preventDefault();
		pesanEmail = "";
		pesanPassword = ""
		if (!email.includes("@")) {
			pesanEmail = "Invalid email format"
		}
		loading = true;
		const { data, error } = await supabase.auth.signInWithPassword({ email, password });
		loading = false;
		if (error) {
			pesanPassword = "Incorrect email or password"
		}
	}
</script>

<form onsubmit={login} novalidate
class="flex w-full max-w-md flex-col gap-4 rounded-xl border border-accent bg-card shadow-lg p-4"
>
	<h1 class="text-4xl font-bold text-primary">StockTrail</h1>
	<div>
		<p class="text-[26px] font-medium">Login</p>
		<p class="text-[14px] text-black/60">Use the account provided by the admin.</p>
	</div>

	<div class="flex flex-col gap-1.5">
		<label for="email">Email</label>
		<Input id="email" type="email" bind:value={email} required placeholder="youremail@gmail.com" class="focus-visible:ring-0"></Input>
		{#if pesanEmail}
			<p class="text-sm text-danger">{pesanEmail}</p>
		{:else}
			<p class="text-sm text-danger">{pesanPassword}</p>
		{/if}
	</div>

	<div class="flex flex-col gap-1.5">
		<label for="password">Password</label>
		<Input id="password" type="password" bind:value={password} required placeholder="enter your password" class="focus-visible:ring-0"></Input>
		{#if pesanPassword}
			<p class="text-sm text-danger">{pesanPassword}</p>
		{/if}
	</div>

	<Button type="submit" disabled={loading} class="font-semibold tracking-wide">Login</Button>
</form>