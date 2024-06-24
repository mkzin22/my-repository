<script lang="ts">
	import { data, type Data } from './data';
	import { AppShell } from '@skeletonlabs/skeleton';
	import { AppRail, AppRailTile, AppRailAnchor } from '@skeletonlabs/skeleton';
	let currentTile: number = 0;
	import  logoEnem  from '$lib/enem-2566.png';
	import gitHub from '$lib/icons8-github-48.png';
	import livros from '$lib/icons8-books-50.png';
	import navBar from '$lib/icons8-cardápio-32.png';
	import redacao from '$lib/icons8-redação-48.png'
	import matematica from '$lib/icons8-matemática-48.png';
	import cN from "$lib/icons8-física-50.png";
	import cH from "$lib/icons8-geografia-48.png"

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
	<svelte:fragment slot="header"><div class=" bg-primary-700 flex-row py-2"><h1 class="font-sans text-2xl text-center italic font-semibold tracking-wider ">Calculadora</h1><img class="object-contain h-15 w-56 m-auto" src="{logoEnem}" alt="Logo Enem"></div></svelte:fragment>
	<svelte:fragment slot="sidebarLeft"><AppRail>
		<svelte:fragment slot="lead">
			<AppRailAnchor href="/" ><img class='m-auto' src="{navBar}" alt="barra de navegação"></AppRailAnchor>
		</svelte:fragment>
		<!-- --- -->
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
			<AppRailAnchor href="/" target="_blank" title="Account"><img src="{gitHub}" alt="Git username" class="py-8 m-auto"></AppRailAnchor>
		</svelte:fragment>
	</AppRail></svelte:fragment>
	<!-- (sidebarRight) -->
	<!-- (pageHeader) -->
	<!-- Router Slot -->

	<p class="text-center py-8"> Faça a simulação da sua nota do enem, caso você tivesse acertado determinado número de questões </p>

	<table>
		<tr>
			<th class="bg-primary-700 py-3">Prova do Enem</th><th class="bg-primary-700">Nota mínima</th><th class="bg-primary-700">Sua nota</th><th class="bg-primary-700">Peso</th><th class="bg-primary-700">Nota com peso</th>
		</tr>
		{#each arr as materia}
			<tr>
				<td>{materia.prova}</td>
				<td><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-36" type="number" placeholder="0.01" bind:value={materia.minGrade} /></td>
				<td><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-36" type="number" placeholder="780.00" bind:value={materia.nota} /></td>
				<td><input class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-36" type="number" placeholder="1.50" bind:value={materia.peso} /></td>
				<td >{calcularNota(materia)}</td>
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
		<td><i>Nota do estudante (B/A) = {calcularScoreFinal(arr).toFixed(2)}</i></td>
	</table>
	<h3>Com base nos dados entre 2020 e 2023</h3>
	{#each mathGrade as m}
		<p>Caso você tivesse acertado {m[0]} questões em matemática sua nota seria:</p>
		Entre {calcularSimulation(arr, m[1]).toFixed(2)} e {calcularSimulation(arr, m[3]).toFixed(2)}
		<br />
		com média de {calcularSimulation(arr, m[2]).toFixed(2)}
	{/each}
	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter">Page Footer</svelte:fragment>
	<svelte:fragment slot="footer">Footer</svelte:fragment>
</AppShell>
