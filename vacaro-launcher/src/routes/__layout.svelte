<script lang="ts">
	import {
		Header,
		HeaderNav,
		HeaderNavItem,
		HeaderNavMenu,
		SkipToContent,
		Content,
		HeaderUtilities,
		HeaderAction,
		HeaderGlobalAction,
		HeaderPanelLinks,
		HeaderPanelDivider,
		HeaderPanelLink,
		SideNav,
		SideNavItems,
		SideNavMenu,
		SideNavMenuItem,
		SideNavLink,
		SideNavDivider
	} from 'carbon-components-svelte';
	import { onMount } from 'svelte';
	import WindowMinimizeButton from '../components/icon/WindowMinimizeButton.svelte';
	import WindowCloseButton from '../components/icon/WindowCloseButton.svelte';

	import WindowMaximizeButton from '../components/icon/WindowMaximizeButton.svelte';

	// import CheckboxUndeterminate from 'carbon-icons-svelte/lib/Checkbox.svelte';

	import CheckBox from 'carbon-icons-svelte/lib/CheckBox.svelte';
	import Settings from 'carbon-icons-svelte/lib/Settings.svelte';
	import Close from 'carbon-icons-svelte/lib/Close.svelte';
	import Minimize from 'carbon-icons-svelte/lib/Minimize.svelte';
	import Maximize from 'carbon-icons-svelte/lib/Maximize.svelte';
	import MoonThemeSwitchIcon from 'carbon-icons-svelte/lib/Moon.svelte';
	import SunThemeSwitchIcon from 'carbon-icons-svelte/lib/Sun.svelte';
	import Fade from 'carbon-icons-svelte/lib/Fade.svelte';
	import HeaderNavItemHref from '../components/navigation/HeaderNavItemHref.svelte';

	import ContextMenuLayout from '../components/ContextMenuLayout.svelte';

	let isOpen = false;
	let isSideNavOpen = false;

	var themeBool = new Boolean(false);
	let themeKey = 'g10';
	let themeBackground = 'filter: invert(-1);';

	onMount(() => {
		if (themeBool == true) {
			themeKey = 'g10';
			themeBackground = 'filter: invert(-1);';
		} else if (themeBool == false) {
			themeKey = 'g90';
			themeBackground = 'filter: invert(1);';
		}
		document.documentElement.setAttribute('theme', themeKey);
	});

	// import { appWindow } from '@tauri-apps/api/window';

	function closeApp() {
		onMount(() => {
			// appWindow.close();
		});
	}

	function themeChange() {
		if (themeBool == true) themeBool = false;
		else if (themeBool == false) themeBool = true;

		if (themeBool == true) {
			themeKey = 'g10';
			themeBackground = 'filter: invert(-1);';
		} else if (themeBool == false) {
			themeKey = 'g90';
			themeBackground = 'filter: invert(1);';
		}
		document.documentElement.setAttribute('theme', themeKey);
	}
</script>

<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/carbon-components-svelte/css/all.css" />
	{#if themeBool === true}
		<link rel="stylesheet" href="https://unpkg.com/@carbon/charts/styles-g90.css" />
	{:else}
		<link rel="stylesheet" href="https://unpkg.com/@carbon/charts/styles-g10.css" />
	{/if}
</svelte:head>

<div>
	<Header
		data-tauri-drag-region
		class="titlebar"
		company="Tauri"
		platformName="Carbon App"
		bind:isSideNavOpen
	>
		<svelte:fragment slot="skip-to-content">
			<SkipToContent />
		</svelte:fragment>

		<HeaderNav data-tauri-drag-region>
			<HeaderNavItemHref Href="/" Text="Dashboard" StartsWith="false" />
			<HeaderNavItemHref Href="/intergrations" Text="Intergrations" StartsWith="false" />
			<HeaderNavItemHref Href="/demographic" Text="Demographic" StartsWith="true" />
			<HeaderNavMenu text="Documentation">
				<HeaderNavItemHref Href="/docs/getting-started" Text="Getting Started" StartsWith="true" />
				<HeaderNavItemHref
					Href="/docs/account-managment"
					Text="Account Management"
					StartsWith="false"
				/>
				<HeaderNavItemHref Href="/docs/self-hosting" Text="Self Hosting" StartsWith="false" />
			</HeaderNavMenu>
		</HeaderNav>
		<HeaderUtilities data-tauri-drag-region>
			{#if themeBool == true}
				<HeaderGlobalAction
					on:click={() => themeChange()}
					aria-label="Toggle Theme"
					icon={MoonThemeSwitchIcon}
				/>
			{:else}
				<HeaderGlobalAction
					on:click={() => themeChange()}
					aria-label="Toggle Theme"
					icon={SunThemeSwitchIcon}
				/>
			{/if}

			<HeaderGlobalAction aria-label="Settings" icon={Settings} />
			<HeaderAction bind:isOpen data-tauri-drag-region>
				<HeaderPanelLinks>
					<HeaderPanelDivider>Switcher subject 1</HeaderPanelDivider>
					<HeaderPanelLink>Switcher item 1</HeaderPanelLink>
					<HeaderPanelDivider>Switcher subject 2</HeaderPanelDivider>
					<HeaderPanelLink>Switcher item 1</HeaderPanelLink>
					<HeaderPanelLink>Switcher item 2</HeaderPanelLink>
					<HeaderPanelLink>Switcher item 3</HeaderPanelLink>
					<HeaderPanelLink>Switcher item 4</HeaderPanelLink>
					<HeaderPanelLink>Switcher item 5</HeaderPanelLink>
				</HeaderPanelLinks>
			</HeaderAction>
		</HeaderUtilities>
		<style>
			.closebutton {
				height: 30px;
				top: 0;
				color: white;
				fill: transparent !important;
				margin-bottom: 17px;
			}
			.closebutton:hover {
				background-color: #e81123;
			}
			.closebutton:focus {
				border: 1px solid solid var(--cds-ui-background);
			}
			.utilbutton {
				height: 30px;
				top: 0;
				margin-bottom: 17px;
				color: white;
				fill: transparent !important;
			}
			.utilbutton:hover {
				background-color: #262626;
			}
			.utilbutton:focus {
				border: 1px solid solid var(--cds-ui-background);
			}
		</style>
		<div
			style="width=100%; margin-left: 20px; margin-right: 1.5px; height=100%"
			data-tauri-drag-region={true}
		>
			<HeaderGlobalAction aria-label="Minimize" class="utilbutton" icon={WindowMinimizeButton} />
			<HeaderGlobalAction aria-label="Maximize" class="utilbutton" icon={WindowMaximizeButton} />
			<HeaderGlobalAction
				on:click={closeApp}
				aria-label="Close"
				class="closebutton"
				icon={WindowCloseButton}
			/>
		</div>
	</Header>

	<SideNav rail bind:isOpen={isSideNavOpen} style={themeBackground}>
		<SideNavItems>
			<SideNavLink icon={Fade} text="Link 1" href="/" isSelected />
			<SideNavLink icon={Fade} text="Link 2" href="/" />
			<SideNavLink icon={Fade} text="Link 3" href="/" />
			<SideNavMenu icon={Fade} text="Menu">
				<SideNavMenuItem href="/" text="Link 1" />
				<SideNavMenuItem href="/" text="Link 2" />
				<SideNavMenuItem href="/" text="Link 3" />
			</SideNavMenu>
			<SideNavDivider />
			<SideNavLink icon={Fade} text="Link 4" href="/" />
		</SideNavItems>
	</SideNav>

	<ContextMenuLayout />

	<Content>
		<slot />
	</Content>

	<style>
		.titlebar {
			height: 32px;
			user-select: none;
		}
		.titlebar-button {
			display: inline-flex;
			justify-content: center;
			align-items: center;
			width: 30px;
			height: 30px;
		}
		.titlebar-button:hover {
			background: #5bbec3;
		}
	</style>
</div>
