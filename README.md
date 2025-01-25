# temperature-converter-web
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Temperature Converter</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        form {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        input, select, button {
            padding: 10px;
            font-size: 16px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 20px;
            padding: 10px;
            background-color: #e7e7e7;
            border-radius: 4px;
            text-align: center;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Temperature Converter</h1>
        <form id="converter-form">
            <input type="number" id="temperature" placeholder="Enter temperature" required step="any">
            <select id="from-unit">
                <option value="celsius">Celsius</option>
                <option value="fahrenheit">Fahrenheit</option>
                <option value="kelvin">Kelvin</option>
            </select>
            <select id="to-unit">
                <option value="fahrenheit">Fahrenheit</option>
                <option value="celsius">Celsius</option>
                <option value="kelvin">Kelvin</option>
            </select>
            <button type="submit">Convert</button>
        </form>
        <div id="result"></div>
    </div>

    <script>
        function convertTemperature(value, fromUnit, toUnit) {
            if (fromUnit === toUnit) return value;
            
            switch (fromUnit) {
                case 'celsius':
                    if (toUnit === 'fahrenheit') return (value * 9/5) + 32;
                    if (toUnit === 'kelvin') return value + 273.15;
                    break;
                case 'fahrenheit':
                    if (toUnit === 'celsius') return (value - 32) * 5/9;
                    if (toUnit === 'kelvin') return (value - 32) * 5/9 + 273.15;
                    break;
                case 'kelvin':
                    if (toUnit === 'celsius') return value - 273.15;
                    if (toUnit === 'fahrenheit') return (value - 273.15) * 9/5 + 32;
                    break;
            }
        }

        document.getElementById('converter-form').addEventListener('submit', function(e) {
            e.preventDefault();
            const temperature = parseFloat(document.getElementById('temperature').value);
            const fromUnit = document.getElementById('from-unit').value;
            const toUnit = document.getElementById('to-unit').value;
            
            if (isNaN(temperature)) {
                document.getElementById('result').textContent = 'Please enter a valid number';
                return;
            }

            const convertedTemp = convertTemperature(temperature, fromUnit, toUnit);
            const result = `${temperature}° ${fromUnit.charAt(0).toUpperCase() + fromUnit.slice(1)} is ${convertedTemp.toFixed(2)}° ${toUnit.charAt(0).toUpperCase() + toUnit.slice(1)}`;
            document.getElementById('result').textContent = result;
        });
    </script>
</body>
</html>
