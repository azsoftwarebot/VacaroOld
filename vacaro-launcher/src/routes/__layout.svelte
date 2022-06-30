<script lang="ts">
	import 'carbon-components-svelte/css/all.css';
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
	import { appWindow } from '@tauri-apps/api/window';

	import WindowMinimizeButton from '../components/icon/WindowMinimizeButton.svelte';
	import WindowCloseButton from '../components/icon/WindowCloseButton.svelte';
	import WindowMaximizeButton from '../components/icon/WindowMaximizeButton.svelte';
	import WindowRestoreButton from '../components/icon/WindowRestoreButton.svelte';
	import WindowMenuIconButton from '../components/icon/WindowMenuIconButton.svelte';

	import Settings from 'carbon-icons-svelte/lib/Settings.svelte';
	import MoonThemeSwitchIcon from 'carbon-icons-svelte/lib/Moon.svelte';
	import SunThemeSwitchIcon from 'carbon-icons-svelte/lib/Sun.svelte';
	import Fade from 'carbon-icons-svelte/lib/Fade.svelte';
	import HeaderNavItemHref from '../components/navigation/HeaderNavItemHref.svelte';

	import ContextMenuLayout from '../components/ContextMenuLayout.svelte';

	let isOpen = false;
	let isSideNavOpen = false;

	var themeBool = new Boolean(true);
	let themeKey = 'g10';

	onMount(() => {
		if (themeBool == true) {
			themeKey = 'g10';
		} else if (themeBool == false) {
			themeKey = 'g90';
		}
		document.documentElement.setAttribute('theme', themeKey);
	});

	function closeApp() {
		appWindow.close();
	}
	function minimizeApp() {
		appWindow.minimize();
	}
	function maximizeApp() {
		appWindow.maximize();
	}
	function restoreApp() {
		appWindow.unmaximize();
	}

	import GetisMaximized from '../components/MaximizeHandler';

	GetisMaximized();

	function themeChange() {
		if (themeBool == true) themeBool = false;
		else if (themeBool == false) themeBool = true;

		if (themeBool == true) {
			themeKey = 'g10';
		} else if (themeBool == false) {
			themeKey = 'g90';
		}
		document.documentElement.setAttribute('theme', themeKey);
	}
</script>

<div>
	<Header
		data-tauri-drag-region
		class="titlebar"
		company="Vacaro"
		platformName="Launcher"
		bind:isSideNavOpen
		iconMenu={WindowMenuIconButton}
		persistentHamburgerMenu
	>
		<svelte:fragment slot="skip-to-content">
			<SkipToContent />
		</svelte:fragment>

		<HeaderNav data-tauri-drag-region>
			<HeaderNavItemHref Href="/" Text="Home" StartsWith="false" />
			<HeaderNavItemHref Href="/engine" Text="Engine" StartsWith="false" />
			<HeaderNavItemHref Href="/assets" Text="Assets" StartsWith="true" />
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
				background-color: #616161;
			}
			.utilbutton:focus {
				border: 1px solid solid var(--cds-ui-background);
			}
		</style>
		<div
			style="width=100%; margin-left: 20px; margin-right: 1.5px; height=100%"
			data-tauri-drag-region={true}
		>
			<HeaderGlobalAction
				aria-label="Minimize"
				on:click={minimizeApp}
				class="utilbutton"
				icon={WindowMinimizeButton}
			/>
			{#if true == true}
				<HeaderGlobalAction
					aria-label="Maximize"
					on:click={maximizeApp}
					class="utilbutton"
					icon={WindowMaximizeButton}
				/>
			{:else}
				<HeaderGlobalAction
					aria-label="Restore"
					on:click={restoreApp}
					class="utilbutton"
					icon={WindowRestoreButton}
				/>
			{/if}
			<HeaderGlobalAction
				on:click={closeApp}
				aria-label="Close"
				class="closebutton"
				icon={WindowCloseButton}
			/>
		</div>
	</Header>

	<SideNav rail bind:isOpen={isSideNavOpen}>
		<!-- style={themeBackground} -->
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
