<script>
	import { phone, code, focused } from '../stores/input';
	import { router } from '../stores/router';
	import { onMount } from 'svelte';
	import InputCode from '../components/ui-kit/inputs/input-code.svelte';
	import telegramApi from '../services/TelegramApi';

	onMount(() => {
		setTimeout(() => {
			focused.set('code');
		}, 0);
	});

	code.subscribe(code => {
		if (code.length > 4) {
			telegramApi.profileManager
				.signIn(code)
				.then(res => {
					router.setRoute('chat-page');
				})
				.catch(err => {
					if (err === 'PHONE_NUMBER_UNOCCUPIED') {
						router.setRoute('register-page');
					} else if (err.type === 'SESSION_PASSWORD_NEEDED') {
						router.setRoute('login-password');
					} else {
						showInvalid();
					}
				});
		}
	});
</script>

<form on:submit="{e => e.preventDefault()}" action="code">
	<h1>{$phone}</h1>
	<div class="hint">We have sent you an SMS with code</div>
	<div class="input-group">
		<InputCode />
	</div>
</form>

<style>
	.hint {
		color: var(--dark-gray);
		font-weight: 400;
		font-size: var(--font-size-medium);
		width: 50%;
		margin-bottom: 4vh;
	}

	form {
		display: flex;
		align-items: center;
		flex-direction: column;
		margin-top: 25vh;
		width: 400px;
		text-align: center;
	}
</style>
