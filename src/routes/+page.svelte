<script>
	import { onMount } from 'svelte';
	import axios from 'axios';
	import WeatherCard from '$lib/components/WeatherCard.svelte';

	let city = '';
	let weatherData = null;
	let error = null;
	async function fetchWeather() {
		try {
			const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=API_KEY&units=metric`);
			weatherData = response.data;
			error = null;
		} catch (err) {
			error = 'City not found or API error';
			weatherData = null;
		}
	}
</script>

<main class="container mx-auto p-4">
	<h1 class="text-3xl font-bold mb-4">Weather Dashboard</h1>

	<div class="form-control">
		<div class="input-group">
			<input type="text" bind:value={city} placeholder="Enter city name" class="input input-bordered" />
			<button class="btn btn-primary" on:click={fetchWeather}>Search</button>
		</div>
	</div>

	{#if error}
		<p class="text-error mt-4">{error}</p>
	{/if}

	{#if weatherData}
		<WeatherCard {weatherData} />
	{/if}
</main>