<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import { onMount, SvelteComponent } from "svelte";
	import ScrollTop from "$lib/ScrollTop.svelte";
	import DarkModeToggle from "$lib/dark_mode_toggle/DarkModeToggle.svelte";
	import avatar from "/avataaars.svg";
	import Projects from "$lib/Projects.svelte";
	import { fly } from "svelte/transition";
	import { writable } from "svelte/store";
import About from "./about.svelte";
import Layout from "./__layout.svelte";
import { element, loop_guard } from "svelte/internal";
import Project from "$lib/Project.svelte";

	
	let returnToTopHidden: boolean = true;
	let y: number;
	let mounted: boolean = false;
	let socialTitle: string = "Socials";
	let aboutMeY: number;
	
		
	onMount(async () => {
		mounted = true;
		const element: HTMLElement = window.document.getElementById("AboutMe");
	})

	// $: y, mounted && y >= 1500 ? returnToTopHidden = false : returnToTopHidden = true;
	$: y, toggleRTT();
	$: y, reveal();

	async function toggleNavBar() {
		if (y >= 1500) {

		}
	}

	async function toggleRTT(): Promise<void> {
		if (mounted) {
			const element: HTMLElement = window.document.getElementById("AboutMe");
			y >= element.getBoundingClientRect().top + y ? returnToTopHidden = false : returnToTopHidden = true;
			returnToTopHidden ? aboutMeReveal = true : aboutMeReveal = false;
		}

	}

	async function getElHeight() {
		let height: number = 0;
		let docHeight: number = 0;
		if (mounted)
		{

			const el: HTMLElement = window.document.getElementById("portfolio");
			docHeight = el.getBoundingClientRect().top;

			const element: HTMLElement = window.document.getElementById("AboutMe");
			if (element) {
				const elHeight: number = element.getBoundingClientRect().top;
				height = elHeight;
			}

			

		}
		return [height, docHeight];
	}

	let aboutMeReveal: boolean = false;

	async function reveal(): Promise<void> {
		if (mounted) {
			const element: HTMLElement = window.document.getElementById("AboutMe");
			if (y >= element.getBoundingClientRect().top + y) {
				aboutMeReveal = true;
			}
		}
		aboutMeReveal = false;
	}

	let AboutMeSelected: HTMLElement;
	let AboutMeTitle: string;

	async function OnAboutMeSelect(id: string): Promise<void> {
		if (AboutMeSelected && AboutMeSelected.id == id) { return; }

		const element: HTMLElement = window.document.getElementById(id);
		element.classList.toggle("bg-blue-500");
		element.classList.toggle("font-semibold");

		const aboutMeEl: HTMLElement = window.document.getElementById("AboutMeBox");
		aboutMeEl.removeChild;
		let heading: HTMLElement = document.createElement("h3");
		heading.innerHTML = id;
		let para: HTMLElement = document.createElement("p");
		para.innerHTML = "text";

		AboutMeTitle = id;

		aboutMeEl.classList.toggle("hidden");

		AboutMeSelected.classList.toggle("bg-blue-500");
		AboutMeSelected.classList.toggle("font-semibold");
		AboutMeSelected = element;
	}



	

	


	// function handleScroll() {
	// 	if (mounted) {
	// 		if ( window.scrollY <= AboutMeEl.getBoundingClientRect().top) {
	// 			returnToTopHidden = true;
	// 		} else {
	// 			returnToTopHidden = false;
	// 		}
	// 	}
	// }

</script>

<svelte:window bind:scrollY={y}/>

<svelte:head>
	<title>Home</title>
</svelte:head>

<!-- {#key y}
	<div id="de" class="sticky top-10 bg-white">
		y: {y}
		{#await getElHeight() then value}
		elHeight: {value[0] + y}, 
		docHeight: {value[1]}
		{/await}
	</div>
{/key} -->

<div id="portfolio" class="bg-gradient-to-r from-amber-200 to-red-200
dark:from-sky-900 dark:to-indigo-900 dark:text-white font-normal overflow-y-scroll snap-mandatory snap-y">

	{#if y >= 0}
	<section id="hero" class="md:flex h-screen md:items-center min-h-screen py-[5.6rem] snap-start" transition:fly={{ x: -400, delay: 100, duration: 1500 }}>
		<div class="max-w-md md:max-w-full md:mx-0 overflow-hidden">
			<div class="md:flex">
				<div class="md:p-8">
					<div>
	
						<h1 class="text-4xl md:text-6xl font-bold mb-[3.2rem] md:text-left text-justify">
	
							Hi, my name is <span class="text-cyan-500 bg-clip-text text-transparent bg-gradient-to-r from-pink-500 to-violet-500 hover:from-blue-500 hover:to-cyan-500">Jaydon</span>
							<br />
							<span class="text-xl md:text-4xl">I'm a Software Engineeering student and software development enthusiast</span>
						</h1>
	
						<div class="md:inline-flex flex flex-col md:flex-row mx-auto md:space-x-4  md:max-w-full max-w-md absolute bottom-8 left-0 right-0 md:static">
	
							<button class="btn-hero" on:click={() => window.document.getElementById("AboutMe").scrollIntoView({behavior: "smooth", block: "start", inline: "nearest"})}>About Me</button>
					
							<button class="btn-hero">My Projects</button>
				
							<DarkModeToggle class="btn-hero w-[48px] "/>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
	{/if}

	
	<section id="AboutMe" class="md:flex h-screen md:items-center min-h-screen py-[5.6rem] snap-start" >
		{#if y >= 1000}
		<div class="w-full  rounded-xl" transition:fly={{ x: -400, delay: 100, duration: 1500 }}>
			<div class="py-6 md:py-8">
				<h2 class="text-center text-3xl md:text-4xl font-bold">About Me</h2>

			</div>

			<div class="w-full inline-flex">

				<div class="ml-auto mr-0 bg-white dark:bg-[#2b2d3b] shadow-md rounded-lg mb-4 p-3 relative">

					<p class="absolute text-center inset-x-0 -top-4">
						<span class="bg-red-300 rounded-full px-1 py-0.5 font-semibold text-xs">{socialTitle}</span>
					</p>

					<!-- svelte-ignore a11y-mouse-events-have-key-events -->
					<div class="inline-flex space-x-4">

						<!-- svelte-ignore a11y-mouse-events-have-key-events -->
						<button on:mouseover={async () => socialTitle = "GitHub"} on:mouseout={async () => socialTitle = "Socials"} on:click={async () => window.open("https://github.com/jadocee", "_blank")}>

							<svg class="socials" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"  aria-labelledby="githubBtnTitle"/>
								<title id="githubBtnTitle">@jadocee</title>
							</svg>

						</button>

						<button on:mouseover={async () => socialTitle = "LinkedIn"} on:mouseout={async () => socialTitle = "Socials"} on:click={async () => window.open("https://www.linkedin.com/in/jaydon-cameron/", "_blank")}>
						
							<svg class="socials" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"  aria-labelledby="linkedInBtnTitle"/>
								<title id="linkedInBtnTitle">Jaydon Cameron</title>
							</svg>

						</button>

						<button on:mouseover={async () => socialTitle = "Email"} on:mouseout={async () => socialTitle = "Socials"} on:click={async () => window.open("mailto:jaydoncameron80@protonmail.com", "_blank")}>

							<svg xmlns="http://www.w3.org/2000/svg" class="socials" viewBox="0 0 20 20" role="img" aria-label="emailBtnTitle" >
								<title id="emailBtnTitle">jaydoncameron80@protonmail.com</title>
								<path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
								<path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
							</svg>
						</button>

						<button on:mouseover={async () => socialTitle = "Twitter"} on:mouseout={async () => socialTitle = "Socials"} on:click={async () => window.open("https://twitter.com/JaCee____", "_blank")}>

							<svg class="socials" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"  aria-labelledby="twitterBtnTitle" aria-modal=true/>
								<title id="twitterBtnTitle">@JaCee____</title>
							</svg>
						</button>
					</div>
				</div>
			</div>

			<!-- <div class="md:shrink-0">
				<img class="h-48 object-cover md:h-full md:w-48 mx-auto" src={avatar} alt="avatar">

			</div> -->

			<div class="md:flex w-full inline-flex">

				<div class="p-2 bg-white dark:bg-[#2b2d3b] rounded-xl shadow-md flex flex-col space-y-2 w-1/6 ml-0 mr-auto text-md">
					<div id="University" class="hover:bg-blue-500 opacity-50 rounded-lg p-2 cursor-pointer hover:font-semibold" on:click={async () => await OnAboutMeSelect("University")}>
						<p>University</p>
					</div>

					<div id="2" class="hover:bg-blue-500 opacity-50 rounded-lg p-2 cursor-pointer hover:font-semibold" on:click={async () => await OnAboutMeSelect("2")}>
						<p>University</p>
					</div>

					<div id="1" class="hover:bg-blue-500 opacity-50 rounded-lg p-2 cursor-pointer hover:font-semibold" on:click={async () => await OnAboutMeSelect("1")}>
						<p>University</p>
					</div>
				</div>
				
				<div id="AboutMeBox" class="p-4 w-[80%] h-full whitespace-normal bg-white dark:bg-[#2b2d3b] rounded-lg hidden ml-auto mr-0" transition:fly={{ x: -400, delay: 100, duration: 1500 }}>

					<h3 class="uppercase md:text-2xl text-xl text-violet-500 font-semibold tracking-wide">{AboutMeTitle}</h3>
					
					<p class="sm:text-sm md:text-md lg:text-lg xl:text-xl">text</p>

					
				</div>
				
				
			</div>
			
		</div>
		{/if}
	</section>
	

	<section class="md:flex md:items-center h-screen min-h-screen w-screen py-[5.6rem]">

		<Projects/>


	</section>

</div>


	<div class="sticky bottom-4 right-0 left-0 mx-1">
		<ScrollTop hidden={returnToTopHidden}/>
	</div>
	
	





