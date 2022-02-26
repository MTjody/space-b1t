<script lang="ts">
import PlayerCard from "./PlayerCard.svelte";

let dmg = 0;
let buff = 0;
let activePlayer = 1;
let hp1 = 50;
let hp2 = 50;

function endTurn() {
	if (activePlayer === 1) {
		// active player gets health buff
		hp1 += buff;
		// the other player should receive damage when turn is ended
		hp2 -= dmg;
	} else {
		hp1 -= dmg;
		hp2 += buff;
	}
	activePlayer = activePlayer === 1 ? 2 : 1;
}

</script>

<main>
	
	<PlayerCard flip={true} active={activePlayer === 1} on:endTurn={endTurn} bind:healthBuff={buff} bind:damage={dmg} bind:health={hp1} />

	<PlayerCard active={activePlayer === 2} on:endTurn={endTurn} bind:healthBuff={buff} bind:damage={dmg} bind:health={hp2}/>

</main>

<style>
	main {
		text-align: center;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
	}

</style>
