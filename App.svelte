<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Urbanist&display=swap" rel="stylesheet">
</svelte:head>
<script>
  import Model from "./model.svelte";
  import { jsPDF } from "jspdf";
  let fisen = "Jimi";
  let lasen = "Markov";
  let csen = "Blue";
  let show = false;
  $: fsen = `${fisen} ${lasen}`;
  let age = 0;
  let people = [
    { name: "boshi", id: 2, age: 12 },
    { name: "bosdsdhi", id: 26, age: 212 },
    { name: "boshsaai", id: 22, age: 12 }
  ];
  const genpdf = () => {
    let doc = new jsPDF();
    doc.text(fsen, 20, 10);
    for (let i = 0; i < people.length; i++) {
      doc.text(people[i].name, 20, 20 + i * 10);
    }
    doc.save(fsen + ".pdf");
  };
  const del = id => {
    people = people.filter(p => p.id != id);
  };
  const toggleshow = () => {
    show = !show;
  };

  let num = 0;
  const handleSub = () => {
    console.log(fsen, age, csen);
    let person = { name: fsen, age: age, id: Math.random() };
    people = [person, ...people];
  };
</script>
<Model col="red" {show} on:click={toggleshow} >
<h3>How are yoy</h3>
<p slot="title">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Vel!</p>
</Model>
<main>
<h2 on:click={toggleshow}> {fsen} - {csen} </h2>
<form on:submit|preventDefault={handleSub} >
  <input type="text" bind:value={fisen} class="b" >
  <input type="text" bind:value={lasen} class="b" >
  <input type="text" bind:value={csen} class="b" class:bruno={num>7} class:bomo={num>5}>
  <input type="number" class="b" bind:value={age}>
  
  
  <button class="b" on:click={()=>{num++;}} >Add {num}</button></form><button class="b" on:click={genpdf} >CLick to generate PDF</button>
  {#if num>-1}
  {#each people as p (p.id)}
  <p>{p.name} {p.age}
  <button class="b" on:click={()=> del(p.id)}>delete</button>
  </p> 
  {:else}
  <p>everyone is sleeping i guess</p>
  {/each}
  {/if}
</main>

<style>
  main {
    font-family: "Urbanist", sans-serif;
    text-align: center;
    text-transform: uppercase;
  }
  h2 {
    font-size: 2em;
    color: #000000;
  }
  .b {
    color: white;
    background-color: #ff3e00;
    border: none;
    padding: 1em;
    font-family: inherit;
    font-size: 1em;
    transition: 0.5s;
    margin: 0.4em;
    display: inline-block;
  }
  .b:hover {
    background-color: #f0ff25;
    color: blue;
  }

  .b:focus {
    background-color: #ffefc4;
    color: black;
  }
  .bomo {
    color: palevioletred;
  }
  .bruno {
    color: firebrick;
  }
</style>

