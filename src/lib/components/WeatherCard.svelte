<script>
    export let weatherData;

    function getWeatherEmoji(weatherId) {
        if (weatherId >= 200 && weatherId < 300) return '⛈️';
        if (weatherId >= 300 && weatherId < 400) return '🌧️';
        if (weatherId >= 500 && weatherId < 600) return '🌦️';
        if (weatherId >= 600 && weatherId < 700) return '❄️';
        if (weatherId >= 700 && weatherId < 800) return '🌫️';
        if (weatherId === 800) return '☀️';
        if (weatherId > 800) return '☁️';
        return '🌈';
    }

    $: weatherEmoji = getWeatherEmoji(weatherData.weather[0].id);
</script>

<div class="mt-6">
    <h2 class="text-2xl font-semibold text-gray-800 mb-2">
        {weatherData.name}, {weatherData.sys.country} {weatherEmoji}
    </h2>
    <p class="text-5xl font-bold text-gray-900 mb-4">{Math.round(weatherData.main.temp)}°C</p>
    <p class="text-xl text-gray-700 mb-4 capitalize">{weatherData.weather[0].description}</p>
    <div class="grid grid-cols-2 gap-4">
        <div class="bg-blue-100 p-3 rounded-lg">
            <p class="text-sm text-gray-600">Humidity</p>
            <p class="text-lg font-semibold">💧 {weatherData.main.humidity}%</p>
        </div>
        <div class="bg-green-100 p-3 rounded-lg">
            <p class="text-sm text-gray-600">Wind Speed</p>
            <p class="text-lg font-semibold">💨 {weatherData.wind.speed} m/s</p>
        </div>
        <div class="bg-yellow-100 p-3 rounded-lg">
            <p class="text-sm text-gray-600">Min Temp</p>
            <p class="text-lg font-semibold">🔽 {Math.round(weatherData.main.temp_min)}°C</p>
        </div>
        <div class="bg-red-100 p-3 rounded-lg">
            <p class="text-sm text-gray-600">Max Temp</p>
            <p class="text-lg font-semibold">🔼 {Math.round(weatherData.main.temp_max)}°C</p>
        </div>
    </div>
</div>