<script>
	import { topBar } from './../../stores/topBar.js';
	import { dialogs } from './../../stores/dialogs.js';
	import { clsx } from './../../helpers/index.js';
	import More from 'images/more.svg';
	import Search from 'images/search.svg';
	import { user } from './../../stores/user.js';
	import Avatar from './../avatar/avatar.svelte';
	import './top-bar.scss';
	import { onMount } from 'svelte';
	let status;

	onMount(() => {
		setInterval(() => {
			status = $topBar.status();
		}, 1000);
	});

	$: status = $topBar.status();
</script>

<div class="top-bar">
	<Avatar small photo="{$topBar.photo.src}" title="{$topBar.title}" />
	<div
		class="{clsx('top-bar__online-info', $topBar.online && 'top-bar__online-info_online')}"
	>
		{status}
	</div>

	<div class="name">{$topBar.title}</div>
	<div class="top-bar__search icon">
		<img src="{Search}" />
	</div>
	<div class="top-bar__more icon">
		<img src="{More}" />
	</div>
</div>
