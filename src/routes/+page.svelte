<script>
	import { onMount } from 'svelte';
	import axios from 'axios';
	import WeatherCard from '../components/WeatherCard.svelte';

	let city = '';
	let weatherData = null;
	let error = null;

	async function fetchWeather() {
		try {
			const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://openweathermap.org/&ved=2ahUKEwiQ88OOlc-IAxX9BxAIHUtQF0oQFnoECA0QAQ&usg=AOvVaw018H_9U9cLmoQlvNn8NPy-&units=metric`);
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