<script lang="ts">
	import { data, type Data } from './data';
	import { AppShell } from '@skeletonlabs/skeleton';
	import { AppRail, AppRailTile, AppRailAnchor } from '@skeletonlabs/skeleton';
	let currentTile: number = 0;
	import { AppBar } from '@skeletonlabs/skeleton';
	import { ProgressBar } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import { initializeStores, Drawer, getDrawerStore } from '@skeletonlabs/skeleton';
	initializeStores();

	const drawerStore = getDrawerStore();
	function drawerOpen(): void {
	drawerStore.open({});
}
	import  logoEnem  from '$lib/enem-2566.png';
	import gitHub from '$lib/icons8-github-48.png';
	import livros from '$lib/icons8-books-50.png';
	import navBar from '$lib/icons8-cardápio-48.png';
	import redacao from '$lib/icons8-redação-48.png'
	import matematica from '$lib/icons8-matemática-48.png';
	import cN from "$lib/icons8-física-50.png";
	import cH from "$lib/icons8-geografia-48.png"
	import ufrn from "$lib/logo-ufrn.png";
	import metropole from "$lib/logo-metropole.png";
	import discord from "$lib/icons8-logo-discord-64.png"
	import eCalc from "$lib/e-calc-logo.png"

	let mathGrade: number[][] = [
		[30, 714, 800, 879],
		[35, 760, 850, 932],
		[40, 820, 900, 978],
		[45, 950, 970, 986]
	];

	let arr: Data[] = data;

	function calcularNota(materia: Data) {
		return (materia.nota * materia.peso).toFixed(2);
	}

	function calcularScore(arr: Data[]) {
		return arr.reduce((total, subject) => {
			return total + subject.peso * subject.nota;
		}, 0);
	}

	function calcularSomaDosPesos(arr: Data[]) {
		return arr.reduce((sum, subject) => {
			return Math.round(sum + subject.peso);
		}, 0);
	}

	function calcularScoreFinal(arr: Data[]) {
		return calcularScore(arr) / calcularSomaDosPesos(arr);
	}

	function calcularSimulation(arr: Data[], math: number) {
		const simuArr = JSON.parse(JSON.stringify(arr)).map((n: Data) =>
			n.prova === 'Matemática e suas tecnologias' ? { ...n, nota: math } : n
		);

		return calcularScoreFinal(simuArr);
	}
</script>

<AppShell>
	<svelte:fragment slot="header"><AppBar background="bg-primary-700" gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
		<svelte:fragment slot="lead"><button class="..." on:click={drawerOpen}><img src="{navBar}" alt="Barra de navegação"></button></svelte:fragment>
		<img class="w-96" src="{eCalc}" alt="E-Calc">
		<svelte:fragment slot="trail"><a href="https://discord.gg/q68hXveA"><img class="hover:bg-tertiary-100 rounded-full" src="{discord}" alt="Discord"></a></svelte:fragment>
	</AppBar>
</svelte:fragment>

 <svelte:fragment slot="sidebarLeft"><Drawer><AppRail>

	<AppRailTile bind:group={currentTile} name="tile-1" value={0} title="tile-1">
		<svelte:fragment slot="lead"><img class="m-auto py-2" src="{redacao}" alt="redação"></svelte:fragment>
		<span>Redação</span>
	</AppRailTile>
	<AppRailTile bind:group={currentTile} name="tile-2" value={1} title="tile-2">
		<svelte:fragment slot="lead"><img class="m-auto py-2" src="{livros}" alt="linguagens"></svelte:fragment>
		<span>Linguagens</span>
	</AppRailTile>
	<AppRailTile bind:group={currentTile} name="tile-3" value={2} title="tile-3">
		<svelte:fragment slot="lead"><img class="m-auto py-2" src="{matematica}" alt="matematica"></svelte:fragment>
		<span>matemática</span>
	</AppRailTile>
	<AppRailTile bind:group={currentTile} name="tile-4" value={3} title="tile-4">
		<svelte:fragment slot="lead"><img class="m-auto py-2" src="{cN}" alt="CN"></svelte:fragment>
		<span class="py-1">Ciências da natureza</span>
		
	</AppRailTile>
	
	<AppRailTile bind:group={currentTile} name="tile-5" value={4} title="tile-5">
		<svelte:fragment slot="lead"><img class="m-auto py-2" src="{cH}" alt="CH"></svelte:fragment>
		<span>Ciências humanas</span>
		
	</AppRailTile>
	<!-- --- -->
	<svelte:fragment slot="trail">
		<div class="flex justify-center py-2"><LightSwitch /></div>
		<AppRailAnchor href="/" target="_blank" title="Account"><img src="{gitHub}" alt="Git username" class="py-8 m-auto"></AppRailAnchor>
	</svelte:fragment>
</AppRail></Drawer></svelte:fragment>

	
	<!-- (sidebarRight) -->
	<!-- (pageHeader) -->
	<!-- Router Slot -->

	<p class="text-center py-8"> Faça a simulação da sua nota do enem, com base no determinado número de questões corretas. </p>
	<p class="text-center"> Essa calculadora é focada em </p><br>

	<table class="m-auto variant-ghost-surface text-sm ">
		<tr>
			<th class="bg-primary-700 py-3">Prova do Enem</th><th class="bg-primary-700">Nota mínima</th><th class="bg-primary-700">Sua nota</th><th class="bg-primary-700">Peso</th><th class="bg-primary-700">Nota com peso</th>
		</tr>
		{#each arr as materia}
			<tr>
				<td>{materia.prova}</td>
				<td><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48" type="number" placeholder="0.01" bind:value={materia.minGrade} /></td>
				<td><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48" type="number" placeholder="780.00" bind:value={materia.nota} /></td>
				<td ><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48" type="number" placeholder="1.50" bind:value={materia.peso} /></td>
				<td class="text-center">{calcularNota(materia)}</td>
			</tr>
		{/each}
	
		<tr>
			<td /><td /><td>Total</td><td>Total</td>
		</tr>
		<tr>
			<td /><td /><td>{calcularScore(arr).toFixed(2)}(A)</td><td
				>{calcularSomaDosPesos(arr).toFixed(2)}(B)</td
			>
		</tr>
		<td class="py-3"><i>Nota do estudante (B/A) = {calcularScoreFinal(arr).toFixed(2)}</i></td>
	</table> 

	
	<div class="variant-glass-primary text-center mt-10 py-4">
	<div class=""><h3 class="py-3">Com base nos dados entre 2020 e 2023</h3></div>
	{#each mathGrade as m}
	 <p class="text-center">Caso você tivesse acertado {m[0]} questões em matemática sua nota seria:</p>
		Entre {calcularSimulation(arr, m[1]).toFixed(2)} e {calcularSimulation(arr, m[3]).toFixed(2)}
		<br />
		com média de {calcularSimulation(arr, m[2]).toFixed(2)} 
		<div class="w-96 m-auto py-2"><ProgressBar  value={100} max={100} /> </div>
	{/each} </div>
	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter" > <AppBar background="bg-primary-700" gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
		<svelte:fragment slot="lead"> <img src="{ufrn}" alt="logo ufrn"></svelte:fragment>
		<div class="text-center"><p>Desenvolvido por estudantes do Instituto Metrópole Digital</p><p>© Copyright 2024</p></div>
		<svelte:fragment slot="trail"><img src="{metropole}" alt="logo metropole"></svelte:fragment>
	</AppBar>
</svelte:fragment>
	
</AppShell>
