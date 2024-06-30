<script lang="ts">
  import { data, type Data } from "./data";
  import { AppShell } from "@skeletonlabs/skeleton";
  import { AppRail, AppRailTile, AppRailAnchor } from "@skeletonlabs/skeleton";
  let currentTile: number = 0;
  import { AppBar } from "@skeletonlabs/skeleton";
  import { ProgressBar } from "@skeletonlabs/skeleton";
  import { LightSwitch } from "@skeletonlabs/skeleton";
  import {
    initializeStores,
    Drawer,
    getDrawerStore,
  } from "@skeletonlabs/skeleton";
  initializeStores();

  const drawerStore = getDrawerStore();
  function drawerOpen(): void {
    drawerStore.open({});
  }
  import { Accordion, AccordionItem } from "@skeletonlabs/skeleton";
  import logoEnem from "$lib/enem-2566.png";
  import gitHub from "$lib/icons8-github-48.png";
  import livros from "$lib/icons8-books-50.png";
  import navBar from "$lib/icons8-cardápio-48.png";
  import redacao from "$lib/icons8-redação-48.png";
  import matematica from "$lib/icons8-matemática-48.png";
  import cN from "$lib/icons8-física-50.png";
  import cH from "$lib/icons8-geografia-48.png";
  import ufrn from "$lib/logo-ufrn.png";
  import metropole from "$lib/logo-metropole.png";
  import discord from "$lib/icons8-logo-discord-64.png";
  import eCalc from "$lib/e-calc-logo.png";
  import biologia from "$lib/icons8-biologia-50.png";
  import quimica from "$lib/icons8-sódio-60.png";
  import historia from "$lib/icons8-coliseu-50.png";
  import sociologia from "$lib/icons8-community-64.png";
  import filosofia from "$lib/icons8-filosofia-50.png";
  import duvidas from "$lib/icons8-interview-64.png";
  import melhorar from "$lib/icons8-atualização-64.png";
  import organizacao from "$lib/icons8-organização-50.png";
  import estrategias from "$lib/icons8-negociação-neutra-48.png";

  let mathGrade: number[][] = [
    [30, 714, 800, 879],
    [35, 760, 850, 932],
    [40, 820, 900, 978],
    [45, 950, 970, 986],
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
      n.prova === "Matemática e suas tecnologias" ? { ...n, nota: math } : n
    );

    return calcularScoreFinal(simuArr);
  }
</script>

<AppShell>
  <svelte:fragment slot="header"
    ><AppBar
      background="bg-primary-700"
      gridColumns="grid-cols-3"
      slotDefault="place-self-center"
      slotTrail="place-content-end"
    >
      <svelte:fragment slot="lead"
        ><button class="..." on:click={drawerOpen}
          ><img src={navBar} alt="Barra de navegação" /></button
        ></svelte:fragment
      >
      <img class="w-96" src={eCalc} alt="E-Calc" />
      <svelte:fragment slot="trail"
        ><LightSwitch />
        <a href="https://discord.gg/q68hXveA" target="_blank"
          ><img
            class="hover:bg-tertiary-100 rounded-full"
            src={discord}
            alt="Discord"
          /></a
        ></svelte:fragment
      >
    </AppBar>
  </svelte:fragment>

  <svelte:fragment slot="sidebarLeft"
    ><Drawer>
      <p class="bg-primary-700 py-6 text-center font-bold h4">
        Caso você tenha tirado uma nota ruim em alguma matéria, e quiser
        melhora-lá:
      </p>

      <div
        class=" logo-cloud grid-cols-1 xl:grid-cols-2 2xl:grid-cols-4 gap-0.5"
      >
        <a
          href="https://youtube.com/playlist?list=PLhFNxzLJLH3vMVikOGLmorhohcG0Bk2ow&si=h8kr8GoUU597BQiP"
          target="_blank"
          class="logo-item"
          ><img src={redacao} alt="" />
          <p>Redação</p></a
        >
        <a
          href="https://youtube.com/playlist?list=PLVyIxkvuIqxpOYJyRjx66ZklG0JrIk8ds&si=5jZeTcbyRs-yBF6t"
          target="_blank"
          class="logo-item"
          ><img src={livros} alt="" />
          <p>Linguagens</p></a
        >
        <a
          href="https://youtube.com/playlist?list=PLTPg64KdGgYhYpS5nXdFgdqEZDOS5lARB&si=FB9ucokEv9YOI4GP"
          target="_blank"
          class="logo-item"
          ><img src={matematica} alt="matematica" />
          <p>Matemática</p></a
        >
        <a
          href="https://www.youtube.com/@ProfGuiGoulart/playlists"
          target="_blank"
          class="logo-item"
          ><img src={biologia} alt="biologia" />
          <p>Biologia</p></a
        >
        <a
          href="https://youtube.com/playlist?list=PLnTvCZqHfhNWekai1S9YZLioVkYSDQSqG&si=-kcp9ezJyCL8qlKy"
          target="_blank"
          class="logo-item"
          ><img src={cN} alt="fisica" />
          <p>Física</p></a
        >
        <a
          href="https://www.youtube.com/playlist?list=PL0LfmDSptaT3Lvnf-YsUI18pzihaLPARU"
          target="_blank"
          class="logo-item"
          ><img src={quimica} alt="quimica" />
          <p>Química</p></a
        >
        <a
          href="https://www.youtube.com/c/ProfessorRicardoMarcílio/playlists"
          target="_blank"
          class="logo-item"
          ><img src={cH} alt="Geografia" />
          <p>Geografia</p></a
        >
        <a
          href="https://www.youtube.com/playlist?list=PLMra4G0-Z7pOmDWJfnFQXEG3P17E9erqs"
          target="_blank"
          class="logo-item"
          ><img src={historia} alt="" />
          <p>História</p></a
        >
        <a
          href="https://www.youtube.com/playlist?list=PLMra4G0-Z7pMnBecUK6b8VpwDceBI7xcE"
          target="_blank"
          class="logo-item"
          ><img src={sociologia} alt="sociologia" />
          <p>Sociologia</p></a
        >
        <a
          href="https://www.youtube.com/playlist?list=PLMra4G0-Z7pOBZjKCxen5cRa6iUMAdYKh"
          target="_blank"
          class="logo-item"
          ><img src={filosofia} alt="" />
          <p>Filosofia</p></a
        >
        <a href="https://discord.gg/q68hXveA" target="_blank" class="logo-item"
          ><img src={duvidas} alt="duvidas" />
          <p>Fale conosco</p></a
        >
        <a href="https://github.com/mkzin22" target="_blank" class="logo-item"
          ><img src={gitHub} alt="GitHub" /></a
        >
      </div>

      <p class="text-center py-2 font-bold h3">Dúvidas Pertinentes</p>
      <Accordion autocollapse>
        <AccordionItem>
          <svelte:fragment slot="lead"
            ><img src={melhorar} alt="" /></svelte:fragment
          >
          <svelte:fragment slot="summary"
            ><p>Como ter um bom desempelho no ENEM?</p></svelte:fragment
          >
          <svelte:fragment slot="content"
            ><ul class="list-disc pl-7">
              <li>
                Esteja sempre informado. Vamos começar pela crucial e mais
                importante de todas as dicas: Esteja sempre informado sobre os
                acontecimentos do país e do mundo.
              </li>
              <li>
                Se informe por noticiários, jornais e portais de notícias.
              </li>
              <li>Leia bastante</li>
              <li>Resolva provas de anos anteriores.</li>
              <li>Aprenda, não decore!</li>
            </ul>
            <div class="flex justify-center">
              <button type="button" class="btn variant-filled"
                ><a
                  target="_blank"
                  href="https://vestibular.mundoeducacao.uol.com.br/enem/dicas-para-um-bom-desempenho-no-enem.htm"
                  >leia mais...</a
                ></button
              >
            </div>
          </svelte:fragment>
        </AccordionItem>
        <AccordionItem>
          <svelte:fragment slot="lead"
            ><img src={organizacao} alt="organizacao" /></svelte:fragment
          >
          <svelte:fragment slot="summary"
            ><p>
              Por onde eu posso me organizar melhor para organizar meus estudos?
            </p></svelte:fragment
          >
          <svelte:fragment slot="content"
            ><p>
              Aqui estão alguns dos sites GRATUITOS que podem te auxiliar em sua
              melhora:
            </p>

            <div class="btn-group variant-filled flex justify-center">
              <button
                ><a
                  href="https://app.planejativo.com/?gad_source=1&gclid=CjwKCAjw4f6zBhBVEiwATEHFVgmRj7jpRPokb3cmmsT8Fe9uwkuLisBQwRAGERcwD8eEKzxtVoH3cBoC8gcQAvD_BwE"
                  >Planejativo</a
                ></button
              >
              <button
                ><a href="https://acelerenoenem.com.br">Acelere no ENEM</a
                ></button
              >
              <button
                ><a href="https://repertorioenem.com.br/01-2/"
                  >Repertório ENEM</a
                ></button
              >
            </div>
          </svelte:fragment>
        </AccordionItem>
        <AccordionItem>
          <svelte:fragment slot="lead"
            ><img src={estrategias} alt="estrategias" /></svelte:fragment
          >
          <svelte:fragment slot="summary"
            ><p>
              Como posso ter boas estratégias para me dar bem na hora da prova?
            </p></svelte:fragment
          >
          <svelte:fragment slot="content">
            <p>Pode-se usar algumas estratégias como:</p>
            <ul class="list-disc pl-7">
              <li>Fazer a redação primeiro.</li>
              <li>
                Responder primeiro as perguntas mais faceis, depois as mais
                difíceis.
              </li>
              <li>Não tenha medo de pular questões.</li>
              <li>
                Preste bastante atenção no enunciado e nas alternativas das
                perguntas.
              </li>
              <li>
                Não fique nervoso, caso não consiga fazer uma questão, dê uma
                parada e respire, tome água e relaxe um pouco.
              </li>
            </ul>
            <p class="text-center">
              Você pode ver mais dicas acessando o botão abaixo:
            </p>
            <div class="flex justify-center">
              <button type="button" class="btn variant-filled"
                ><a
                  target="_blank"
                  href="https://aprovatotal.com.br/dicas-enem/">leia mais...</a
                ></button
              >
            </div>
          </svelte:fragment>
        </AccordionItem>
      </Accordion>

      <p class="text-center py-2 font-bold h3">Dicas para arrasar no ENEM</p>

      <ul class="list-disc pl-7 variant-glass-primary py-5 mt-3">
        <li>
          <strong> Faça simulados e cronometre-os!</strong> isso fará com que você tenha mais
          noção de quanto tempo levarás para finalizar uma questão e uma prova.
        </li>
        <li>
          <strong> Na reta final, não passe o dia estudando! </strong>tire um tempo para relaxar
          um pouco e revisar os conteúdos, evite o encarretamento deles!
        </li>
        <li>
          <strong> Leia diversas notícias verídicas! Fuja das Fake News!</strong> Isso ajudará no
          seu desempenho em estruturar de de uma maneira mais fácil e tranquila
          suas redações, sem deixar faltar repertórios.
        </li>
        <li>
          <strong>Adote formas diferentes de estudar!</strong>  não se prenda a uma ou duas, tenha
          diversas estratégias, isso ajudará em seu desempenho e fará com que
          você se canse menos.
        </li>
        <li>
          <strong> Desligue o celular e vá viver a vida!</strong> Parece uma dica simples, mas
          desligar o celular é mais difícil do que parece. Tire uma a duas horas
          do seu dia para mantê-lo desligado, viva em um mundo sem notificações,
          e-mails e whatsapp. Os primeiros dias podem ser um pouco assustadores,
          mas depois você vai entender o porquê. Aproveite uma vida menos
          imediatista para viver melhor, faça caminhadas e outros exercícios,
          conheça o seu bairro e seus vizinhos, invista seu tempo em coisas que
          você tem vontade de fazer e muitas vezes a preguiça ou a tela do
          celular te impedem.
        </li>
      </ul>

	  <p> </p>
    </Drawer></svelte:fragment
  >

  <!-- (sidebarRight) -->
  <!-- (pageHeader) -->
  <!-- Router Slot -->

  <p class="text-center py-8">
    Faça a simulação da sua nota do enem, com base no determinado número de
    questões corretas.
  </p>
  <p class="text-center">Essa calculadora é focada em</p>
  <br />

  <table class="m-auto variant-ghost-surface text-sm">
    <tr>
      <th class="bg-primary-700 py-3">Prova do Enem</th><th
        class="bg-primary-700">Nota mínima</th
      ><th class="bg-primary-700">Sua nota</th><th class="bg-primary-700"
        >Peso</th
      ><th class="bg-primary-700">Nota com peso</th>
    </tr>
    {#each arr as materia}
      <tr>
        <td>{materia.prova}</td>
        <td
          ><input
            class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48"
            type="number"
            placeholder="0.01"
            bind:value={materia.minGrade}
          /></td
        >
        <td
          ><input
            class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48"
            type="number"
            placeholder="780.00"
            bind:value={materia.nota}
          /></td
        >
        <td
          ><input
            class="bg-primary-800 rounded-lg border-blue-400 border-2 m-2 w-16 md:w-48"
            type="number"
            placeholder="1.50"
            bind:value={materia.peso}
          /></td
        >
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
    <td class="py-3"
      ><i>Nota do estudante (B/A) = {calcularScoreFinal(arr).toFixed(2)}</i></td
    >
  </table>

  <div class="variant-glass-primary text-center mt-10 py-4">
    <div class="">
      <h3 class="py-3">Com base nos dados entre 2020 e 2023</h3>
    </div>
    {#each mathGrade as m}
      <p class="text-center">
        Caso você tivesse acertado {m[0]} questões em matemática sua nota seria:
      </p>
      Entre {calcularSimulation(arr, m[1]).toFixed(2)} e {calcularSimulation(
        arr,
        m[3]
      ).toFixed(2)}
      <br />
      com média de {calcularSimulation(arr, m[2]).toFixed(2)}
      <div class="w-96 m-auto py-2"><ProgressBar value={100} max={100} /></div>
    {/each}
  </div>
  <slot />
  <!-- ---- / ---- -->
  <svelte:fragment slot="pageFooter">
    <AppBar
      background="bg-primary-700"
      gridColumns="grid-cols-3"
      slotDefault="place-self-center"
      slotTrail="place-content-end"
    >
      <svelte:fragment slot="lead">
        <a href="https://www.ufrn.br/" target="_blank"><img src={ufrn} alt="logo ufrn" /></a></svelte:fragment
      >
      <div class="text-center">
        <p>Desenvolvido por estudantes do Instituto Metrópole Digital</p>
        <p>© Copyright 2024</p>
      </div>
      <svelte:fragment slot="trail"
        ><a href="https://www.metropoledigital.ufrn.br/portal/" target="_blank"><img src={metropole} alt="logo metropole" /></a></svelte:fragment
      >
    </AppBar>
  </svelte:fragment>
</AppShell>
