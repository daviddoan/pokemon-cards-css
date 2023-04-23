<script>
  import { onMount } from "svelte";

	import Search from "./Search.svelte";
	import CardList from "./Cards.svelte";
	import Card from "./lib/components/CardProxy.svelte";

	let showcase, basics, reverse, holos, cosmos, amazings, radiant, basicGallery, 
			vee, veeUltra, veeAlt, veeMax, veeMaxAlt, veeStar, 
			trainerHolo, rainbow, gold, veeGallery, shinyVault;

	let query = "";
	let isLoading = true;

	const getCards = async () => {
		let promiseArray = [];
		let cardFetch = await fetch("/data/cards.json");
		let cards = await cardFetch.json();
		return cards;
	};

	const loadCards = async() => {
		return getCards()
			.then((cards) => {
				window.cards = cards;
				showcase = cards[0];
				basics = cards.slice(1, 4);
				reverse = [...cards.slice(4, 7), ...cards.slice(70,76)];
				holos = cards.slice(7, 13);
				cosmos = cards.slice(13, 16);
				amazings = cards.slice(76, 85);
				radiant = cards.slice(16, 19);
				basicGallery = cards.slice(19, 22);
				vee = cards.slice(22, 25);
				veeUltra = cards.slice(25, 28);
				veeAlt = cards.slice(28, 34);
				veeMax = cards.slice(37, 40);
				veeMaxAlt = cards.slice(40, 43);
				veeStar = cards.slice(43, 46);
				trainerHolo = cards.slice(46, 52);
				rainbow = cards.slice(52, 58);
				gold = cards.slice(58, 64);
				veeGallery = cards.slice(64, 70);
				shinyVault = cards.slice(85,91);
				isLoading = false;
			});
	};

	onMount(() => {
		loadCards();
		const $headings = document.querySelectorAll("h1,h2,h3");
		const $anchor = [...$headings].filter((el) => {
			const id = el.getAttribute("id")?.replace(/^.*?-/g,"");
			const hash = window.location.hash?.replace(/^.*?-/g,"")
			return id === hash;
		})[0];
		if( $anchor ) {
			setTimeout(() => {
				$anchor.scrollIntoView();
			},100);
		}
	});
</script>

<main>
	<header>
		<h1 id="⚓-top">Congratulations Tony and Margaret!!</h1>
		<section class="intro" id="⚓-intro">
			<p>
				I don't know what to write here because it was a long time coming, but it still doesn't it make it less crazy. I'm really happy for you two and hope that your year abroad is everything you wanted it to be. Thank you for being my friend, and for all the good (and hilarious) memories. - David
			</p>
			<hr>
			<p>
				Thank you for inviting me to the wedding even though we only met a couple of times :) Thank you both for being such good friends to David and for being so welcoming towards me. I'm excited for this new chapter in your lives, and we'll be here to bring more chaos and friendship! Congrats newlyweds! - Mel
			</p>
		<hr>
		</section>

		<div class="showcase">
			{#if !showcase}
				loading...
			{:else}
				<Card
					img = {'https://i.etsystatic.com/icm/6a910f/538287772/icm_fullxfull.538287772_o8andjvkllw4wo8gckkg.png'}
					style = {"sunpillar"}
					rarity = {"rare holo vmax"}
					showcase = {true}
				/>
			{/if}
		</div>

	</header>
</main>

<style>
  .back-to-top a {
    color: inherit;
    text-decoration: none;
		z-index: 999;
  }
</style>
