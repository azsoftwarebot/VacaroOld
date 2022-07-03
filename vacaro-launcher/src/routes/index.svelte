<script>
	import { Grid, Row, Column, Tile, AspectRatio } from 'carbon-components-svelte';
	import FAQ from '../components/home/FAQ.svelte';
	import YT from '../components/home/YT.svelte';
</script>

<Tile>
	<Grid>
		<Row>
			<Column>Column</Column>
			<Column>Column</Column>
			<Column>Column</Column>
			<Column>Column</Column>
		</Row>
	</Grid>
</Tile>

<Grid style="margin-top: 12px; width: 100%;">
	<Row>
		<Column aspectRatio="2x1">
			<AspectRatio ratio="16x9">
				<Tile style="height: 100% !important;">
					<YT title="Music" url="https://www.youtube.com/embed/_8_X-M68c6Q" />
				</Tile>
			</AspectRatio>
		</Column>
		<Column aspectRatio="2x1">
			<FAQ />
		</Column>
	</Row>
</Grid>
