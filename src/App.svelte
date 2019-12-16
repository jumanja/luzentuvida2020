<script>
	import './mystyles.scss';

    import { onMount } from "svelte";

	let color = "";
	let semana = 0;
	let codigo = "";
	let tiempo = "";

	const apiURL = "http://luzentuvida.net/api/v1.5.3/readings?";

	let data = [];

    onMount(async function() {
        const response = await fetch(apiURL);
		data = await response.json();
		color = data[0].color;
		semana = data[0].semana;
		codigo = data[0].codigo;
		tiempo = data[0].tiempo;
    });

</script>
<body class="{'container ' + color}">
<section class="{'container ' + color}">
  <div class="hero-body">
		<div class="card">
			<div class="card-content">
				<div class="media">
				<div class="media-left">
					<figure class="image is-124x124">
					<img src="http://luzentuvida.net/img/Logo_LTV_2014_peque.png" alt="Placeholder image">
					</figure>
				</div>
				<div class="media-content">
					<h1 class="title is-4">LuzEnTuVida.net</h1>
					<p class="subtitle is-5">
							<span >Dios Te Habla Hoy<br></span>
						{#if color != ''}
							<span >Semana {semana}</span>
							<span >{codigo}</span>
						{/if}
					</p>
				</div>
				</div>
			</div>
		</div>

  </div>
</section>
<section class="{'container ' + color}">
  <div class="hero-body">
			<div class="card">
			<div class="card-content">
				<div class="media">
				<div class="media-content">
					{#each data as item }
						<br>
						<h1 class="title"> Primera Lectura, {item.primera_libro} <span class="title is-6">({item.primera})</span> </h1>
						<p class="subtitle"> {item.primera_contenido} </p>
						<p class="title is-5">
							<span class="title is-5">Lector(a): </span> <span class="subtitle is-6">Palabra de Dios</span><br> 
							<span class="title is-5"></span>Todos: <span class="subtitle is-6">Te alabamos, Señor.</span> 
						</p>

						<h1 class="title"> Responsorial: {item.salmo_libro} <span class="title is-6">({item.salmo})</span> </h1>
						<p class="subtitle"> {item.salmo_contenido} </p>
						<p></p>

						{#if item.segunda_contenido != 'empty'}
							<h1 class="title"> Segunda Lectura, {item.segunda_libro} <span class="title is-6">({item.segunda})</span> </h1>
							<p class="subtitle"> {item.segunda_contenido} </p>

							<p class="title is-5">
								<span class="title is-5">Lector(a): </span> <span class="subtitle is-6">Palabra de Dios</span><br> 
								<span class="title is-5"></span>Todos: <span class="subtitle is-6">Te alabamos, Señor.</span> 
							</p>
						{/if}

						<h1 class="title"> El Santo Evangelio según San {item.evangelio_libro} <span class="title is-6">({item.evangelio})</span> </h1>
						<p class="subtitle"> {item.evangelio_contenido} </p>

						
						<p class="title is-5">
							<span class="title is-5">Lector(a): </span> <span class="subtitle is-6">Palabra del Señor</span><br> 
							<span class="title is-5"></span>Todos: <span class="subtitle is-6">Gloria a tí, Señor Jesús.</span> 
						</p>

					{/each}
				</div>
				</div>
			</div>
			</div>

  </div>
</section>
	
</body>
