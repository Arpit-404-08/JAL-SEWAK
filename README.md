
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background: #f0f0f0;
            color: #333;
            margin: 0;
            padding-top: 20px; /* Added padding at the top */
            display: flex;
            flex-direction: column; /* Modified flex direction */
            align-items: center;
        }
        .header {
            background: #4CAF50;
            width: 100%;
            text-align: center;
            padding: 10px 0;
            color: white;
            position: fixed; /* Added fixed positioning */
            top: 0;
            left: 0;
            z-index: 1000; /* Ensuring it stays on top */
        }
        .header div {
            font-size: 24px;
            font-weight: bold;
        }
        .content {
            padding-top: 60px; /* Added padding to offset fixed header */
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            color: #4CAF50;
            margin-bottom: 5px;
            animation: fadeIn 1s ease-in-out;
        }
        h2 {
            color: #666;
            margin-bottom: 20px;
            font-weight: normal;
            animation: fadeIn 1s ease-in-out;
        }
        .data-container {
            background: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 400px;
            width: 100%;
            animation: slideIn 1s ease-in-out;
        }
        .data-container p {
            font-size: 18px;
            margin: 10px 0;
            color: #333;
        }
        .chart-container {
            width: 100%;
            max-width: 600px;
            margin: 20px auto;
        }
        canvas {
            background: #fff;
            border-radius: 10px;
            padding: 10px;
        }
        .footer {
            margin-top: 20px;
            font-size: 14px;
            color: #aaa;
            text-align: center;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes slideIn {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        @media (max-width: 600px) {
            body {
                padding: 20px;
            }
        }
    </style>
    <script>
        async function fetchThingSpeakData() {
            const channelId = '2739296'; // Your actual Channel ID
            const readApiKey = 'J0NT42QJ7Y5MN44E'; // Your actual Read API Key
            const url = `https://api.thingspeak.com/channels/${channelId}/feeds.json?api_key=${readApiKey}&results=10`;

            try {
                const response = await fetch(url);
                const data = await response.json();
                const feeds = data.feeds;

                const labels = feeds.map(feed => new Date(feed.created_at).toLocaleTimeString());
                const phData = feeds.map(feed => feed.field1);
                const tdsData = feeds.map(feed => feed.field2);
                const temperatureData = feeds.map(feed => feed.field3);
                const turbidityData = feeds.map(feed => feed.field4);

                document.getElementById('ph').innerText = `PH: ${phData[phData.length - 1]}`;
                document.getElementById('tds').innerText = `TDS: ${tdsData[tdsData.length - 1]}`;
                document.getElementById('temperature').innerText = `Temperature: ${temperatureData[temperatureData.length - 1]}`;
                document.getElementById('turbidity').innerText = `Turbidity: ${turbidityData[turbidityData.length - 1]}`;

                updateChart(phChart, labels, phData);
                updateChart(tdsChart, labels, tdsData);
                updateChart(temperatureChart, labels, temperatureData);
                updateChart(turbidityChart, labels, turbidityData);
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }

        function updateChart(chart, labels, data) {
            chart.data.labels = labels;
            chart.data.datasets[0].data = data;
            chart.update();
        }

        let phChart, tdsChart, temperatureChart, turbidityChart;

        window.onload = () => {
            const ctxPh = document.getElementById('phChart').getContext('2d');
            phChart = new Chart(ctxPh, {
                type: 'line',
                data: {
                    labels: [],
                    datasets: [{
                        label: 'PH',
                        data: [],
                        backgroundColor: 'rgba(75, 192, 192, 0.2)',
                        borderColor: 'rgba(75, 192, 192, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            const ctxTds = document.getElementById('tdsChart').getContext('2d');
            tdsChart = new Chart(ctxTds, {
                type: 'line',
                data: {
                    labels: [],
                    datasets: [{
                        label: 'TDS',
                        data: [],
                        backgroundColor: 'rgba(255, 99, 132, 0.2)',
                        borderColor: 'rgba(255, 99, 132, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            const ctxTemperature = document.getElementById('temperatureChart').getContext('2d');
            temperatureChart = new Chart(ctxTemperature, {
                type: 'line',
                data: {
                    labels: [],
                    datasets: [{
                        label: 'Temperature',
                        data: [],
                        backgroundColor: 'rgba(255, 206, 86, 0.2)',
                        borderColor: 'rgba(255, 206, 86, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            const ctxTurbidity = document.getElementById('turbidityChart').getContext('2d');
            turbidityChart = new Chart(ctxTurbidity, {
                type: 'line',
                data: {
                    labels: [],
                    datasets: [{
                        label: 'Turbidity',
                        data: [],
                        backgroundColor: 'rgba(153, 102, 255, 0.2)',
                        borderColor: 'rgba(153, 102, 255, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            fetchThingSpeakData();
            setInterval(fetchThingSpeakData, 15000); // Fetch new data every 15 seconds
        };
    </script>
</head>
<body>
    <div class="header">
        <div>Jal Sewak</div>
    </div>
    <div class="content">
        <div class="data-container">
            <h1>Team Data</h1>
            <h2>Collected Data</h2>
            <p id="ph">PH: Loading...</p>
            <p id="tds">TDS: Loading...</p>
            <p id="temperature">Temperature: Loading...</p>
            <p id="turbidity">Turbidity: Loading...</p>
        </div>
        <div class="chart-container">
            <canvas id="phChart"></canvas>
        </div>
        <div class="chart-container">
            <canvas id="tdsChart"></canvas>
        </div>
        <div class="chart-container">
            <canvas id="temperatureChart"></canvas>
        </div>
        <div class="chart-container">
            <canvas id="turbidityChart"></canvas>
        </div>
        <div class="footer">
            <p>Created by Adarsh Srivaatav, Arpit Chaturvedi, Abhinandan, Adarika</p>
        </div>
    </div>
</body>
</html>
