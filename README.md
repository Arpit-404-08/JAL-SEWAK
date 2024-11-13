<!DOCTYPE html>
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
        @keyframes slide
