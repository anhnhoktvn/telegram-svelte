<script>
	import { country, focused } from '../../../stores/input';

	let elem;

	$: $focused === 'country' && elem.focus();

	const onFocus = () => {
		focused.set('country');
	};
</script>

<input
	bind:this="{elem}"
	on:focus="{onFocus}"
	required
	bind:value="{$country}"
	type="country"
/>
<label for="country">Country</label>
<div class="icon">
	<div class="line"></div>
	<div class="line"></div>
</div>

<style lang="scss">
	.icon {
		width: 28px;
		height: 28px;
		position: absolute;
		right: 16px;
		display: flex;
		align-items: center;

		.line {
			transition: transform 0.1s ease-in;
			position: absolute;
			height: 3px;
			width: 16px;
			background-color: #dadce0;
			border-radius: 4px;

			&:first-child {
				left: 2px;
				transform: rotate(45deg);
			}

			&:last-child {
				right: 1px;
				transform: rotate(-45deg);
			}
		}
	}

	input:focus ~ .icon {
		.line {
			&:first-child {
				transform: rotate(-45deg);
			}

			&:last-child {
				transform: rotate(45deg);
			}
		}
	}
</style>
