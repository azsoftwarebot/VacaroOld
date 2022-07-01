<script context="module">
	// @ts-ignore
	export function load({ error, status }) {
		return {
			props: {
				title: `${status}`,
				message: `${error.message}`
			}
		};
	}
</script>

<script>
	export /**
	 * @type {any}
	 */
	let title;

	export let message;
</script>

<h1>{title}</h1>
<p>{message}</p>
