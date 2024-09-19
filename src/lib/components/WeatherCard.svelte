<script>
    export let weatherData;
</script>

<div class="card bg-base-100 shadow-xl mt-4">
    <div class="card-body">
        <h2 class="card-title">{weatherData.name}, {weatherData.sys.country}</h2>
        <p class="text-4xl">{Math.round(weatherData.main.temp)}°C</p>
        <p>{weatherData.weather[0].description}</p>
        <div class="flex justify-between mt-4">
            <div>
                <p>Humidity: {weatherData.main.humidity}%</p>
                <p>Wind: {weatherData.wind.speed} m/s</p>
            </div>
            <div>
                <p>Min: {Math.round(weatherData.main.temp_min)}°C</p>
                <p>Max: {Math.round(weatherData.main.temp_max)}°C</p>
            </div>
        </div>
    </div>
</div>