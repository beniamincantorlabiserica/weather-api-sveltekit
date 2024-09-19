<script>
	import { onMount } from 'svelte';
	import axios from 'axios';
	import WeatherCard from '$lib/components/WeatherCard.svelte';

	let city = '';
	let weatherData = null;
	let error = null;
	let loading = false;
	const API_KEY = import.meta.env.VITE_OPENWEATHER_API_KEY;

	async function fetchWeather() {
		if (!city.trim()) return;
		loading = true;
		try {
			const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather`, {
				params: {
					q: city,
					appid: API_KEY,
					units: 'metric'
				}
			});
			weatherData = response.data;
			error = null;
		} catch (err) {
			console.error('API Error:', err);
			error = 'City not found or API error';
			weatherData = null;
		} finally {
			loading = false;
		}
	}
</script>

<main class="min-h-screen bg-gradient-to-br from-blue-400 to-purple-500 flex flex-col items-center justify-center p-4">
	<div class="bg-white bg-opacity-80 backdrop-blur-md rounded-lg shadow-xl p-8 w-full max-w-md">
		<h1 class="text-4xl font-bold mb-6 text-center text-gray-800">Weather Dashboard 🌦️</h1>

		<div class="form-control">
			<div class="input-group">
				<input
						type="text"
						bind:value={city}
						placeholder="Enter city name"
						class="input input-bordered w-full"
						on:keypress={(e) => e.key === 'Enter' && fetchWeather()}
				/>
				<button class="btn btn-primary" on:click={fetchWeather} disabled={loading}>
					{#if loading}
						<span class="loading loading-spinner"></span>
					{:else}
						🔍
					{/if}
				</button>
			</div>
		</div>

		{#if error}
			<p class="text-error mt-4 text-center">{error}</p>
		{/if}

		{#if weatherData}
			<WeatherCard {weatherData} />
		{:else if !error}
			<p class="text-gray-600 mt-4 text-center">Enter a city to get started! 🏙️</p>
		{/if}
	</div>
</main>