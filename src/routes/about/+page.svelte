<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
	import { base } from "$app/paths";
</script>

<div class="text-column">
	<h1 class="about-me-title">About this project...</h1>

	<p>
		Hi👋 My name is <b>Camila</b>, I'm a software developer who loves to learn new programming languages, frameworks, and any code related stuff.
	</p>
	
	<p>
		This is an easy project I've made to pick up <a href="https://svelte.dev/" target="_blank">Svelte</a>. It was fun learning about it, playing with it, and getting to understand how its <a href="https://svelte.dev/blog/runes" target="_blank">runes</a> work.
	</p>

	<p>
		Whenever I got stuck, I was thankfull to find an answer to some of the issues I faced looking at a similar project that was made in a <a href="https://joyofcode.xyz/svelte-todo-app" target="_blank">Tutorial from JoyOfCode</a>.
	</p>
	<p>
		A <a href="{base}/sverdle">wordle</a> come included with the project when I started, and as a wordle lover I can't simply remove it, so feel free to play with it.
	</p>
</div>

<style>
	.about-me-title{
		font-weight: 600;
		text-shadow: 1.5px 1.5px 6px var(--color-theme-3);
	}
</style>