<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jal Sewak Team Data</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background: #f0f0f0;
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
        }
        .header {
            background: #4CAF50;
            width: 100%;
            text-align: center;
            padding: 10px 0;
            color: white;
        }
        .header div {
            font-size: 24px;
            font-weight: bold;
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
            const url = `https://api.thingspeak.com/channels/${channelId}/feeds.json?api_key=${readApiKey}&results=1`;

            try {
                const response = await fetch(url);
                const data = await response.json();
                const feed = data.feeds[0];
                document.getElementById('ph').innerText = `PH: ${feed.field1}`;
                document.getElementById('tds').innerText = `TDS: ${feed.field2}`;
                document.getElementById('temperature').innerText = `Temperature: ${feed.field3}`;
                document.getElementById('turbidity').innerText = `Turbidity: ${feed.field4}`;
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }

        window.onload = () => {
            fetchThingSpeakData();
            setInterval(fetchThingSpeakData, 1500); // Fetch new data every 15 seconds
        };
    </script>
</head>
<body>
    <div class="header">
        <div>Jal Sewak</div>
    </div>
    <div class="data-container">
        <h1>Team Data</h1>
        <h2>Collected Data</h2>
        <p id="ph">PH: Loading...</p>
        <p id="tds">TDS: Loading...</p>
        <p id="temperature">Temperature: Loading...</p>
        <p id="turbidity">Turbidity: Loading...</p>
    </div>
    <div class="footer">
        <p>Created by Adarsh Srivaatav, Arpit Chaturvedi, Abhinandan, Adarika, Ankit</p>
    </div>
</body>
</html>
