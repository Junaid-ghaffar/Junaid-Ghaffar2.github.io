<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cat Facts</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        table, th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        img {
            max-width: 300px;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Cat Facts</h1>

    <button onclick="fetchCatFacts()">Get Cat Facts</button>

    <table id="factsTable">
        <thead>
            <tr>
                <th>Fact ID</th>
                <th>Fact</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <img id="catImage" src="https://via.placeholder.com/300" alt="Cat Image">

    <script>
        async function fetchCatFacts() {
            try {
                const response = await fetch('https://brianobruno.github.io/cats.json');
                const data = await response.json();
                const sortedFacts = data.facts.sort((a, b) => a.factId - b.factId);
                const tableBody = document.getElementById('factsTable').querySelector('tbody');
                tableBody.innerHTML = '';

                sortedFacts.forEach(fact => {
                    const row = document.createElement('tr');
                    const factIdCell = document.createElement('td');
                    const factCell = document.createElement('td');

                    factIdCell.textContent = fact.factId;
                    factCell.textContent = fact.fact;
                    
                    row.appendChild(factIdCell);
                    row.appendChild(factCell);
                    tableBody.appendChild(row);
                });

                document.getElementById('catImage').src = data.imageURL;

            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }
    </script>

</body>
</html>
