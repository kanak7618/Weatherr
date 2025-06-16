<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Weather App</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }
    body {
      background: linear-gradient(135deg, #74ebd5, #ACB6E5);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: #333;
      text-align: center;
      padding: 20px;
    }
    h1 {
      font-size: 3rem;
      margin-bottom: 20px;
      color: #fff;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    input {
      padding: 12px 20px;
      width: 260px;
      border: none;
      border-radius: 30px;
      outline: none;
      margin-bottom: 15px;
      font-size: 1rem;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      transition: 0.3s;
    }
    input:focus {
      transform: scale(1.05);
    }
    button {
      padding: 12px 30px;
      border: none;
      border-radius: 30px;
      background-color: #fff;
      color: #74ebd5;
      font-weight: bold;
      font-size: 1rem;
      cursor: pointer;
      transition: all 0.3s ease;
      margin-bottom: 20px;
    }
    button:hover {
      background-color: #74ebd5;
      color: #fff;
      transform: scale(1.05);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
    }
    .weather-result {
      font-size: 1.5rem;
      background: rgba(255, 255, 255, 0.8);
      padding: 20px 30px;
      border-radius: 20px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
      animation: fadeIn 1s ease-in;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

  <h1>Weather App 🌤️</h1>
  <input type="text" id="cityInput" placeholder="Enter city name..." />
  <button onclick="getWeather()">Get Weather</button>

  <div class="weather-result" id="weatherResult"></div>

  <script>
    async function getWeather() {
      const city = document.getElementById('cityInput').value.trim();
      if (city === '') {
        alert('Please enter a city name');
        return;
      }

      const apiKey = 'ec18a2ed361fb6e570b93fb6739c0ee6'; 
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const response = await fetch(url);
        const data = await response.json();
        if (data.cod === 200) {
          document.getElementById('weatherResult').innerHTML = `
            <strong>🌍 City:</strong> ${data.name} <br>
            <strong>🌡️ Temp:</strong> ${data.main.temp}°C <br>
            <strong>🌫️ Weather:</strong> ${data.weather[0].description}
          `;
        } else {
          document.getElementById('weatherResult').innerHTML = "❌ City not found.";
        }
      } catch (error) {
        console.error(error);
        document.getElementById('weatherResult').innerHTML = "⚠️ Error fetching data.";
      }
    }
  </script>

</body>
</html>
