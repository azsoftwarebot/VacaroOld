<script>
	import {
		ButtonSet,
		Button,
		Dropdown,
		Tile,
		ImageLoader,
		InlineNotification
	} from 'carbon-components-svelte';
	var key = 0;
</script>

<Tile>
	<!-- <Button
		kind="ghost"
		on:click={() => {
			key++;
		}}>Reload image</Button
	> -->
	<div class="center">
		<InlineNotification
			class="warning-card"
			lowContrast
			kind="warning"
			title="Scheduled maintenance:"
			subtitle="Maintenance will last 2-4 hours."
		/>
	</div>
	{#key key}
		<ImageLoader
			fadeIn
			ratio="16x9"
			src="https://cdn.discordapp.com/attachments/281535090134351874/974038871811690516/4.jpg"
		/>
	{/key}
	<ButtonSet>
		<Dropdown
			hideLabel
			titleText="Engine Version"
			selectedId="0"
			items={[
				{ id: '0', text: '0.0.1' },
				{ id: '1', text: '0.0.2 Beta' },
				{ id: '2', text: '0.0.3 Alpha' }
			]}
		/>

		<Button>Submit</Button>
	</ButtonSet>
</Tile>
