---
layout: page
icon: fas fa-search
order: 5
title: ICD-10 Search
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ICD-10 Code Search</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            color: #1f2937;
        }
    </style>
</head>
<body class="bg-gray-100 min-h-screen flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl shadow-xl w-full max-w-2xl overflow-hidden">
        <div class="p-6 md:p-8">
            <h1 class="text-3xl font-bold mb-2 text-center text-gray-800">ICD-10 Code Search</h1>
            <p class="text-gray-500 mb-6 text-center">
                Search for ICD-10 codes by description.
            </p>
            
            <!-- Search Input -->
            <div class="mb-6">
                <input
                    type="text"
                    id="searchInput"
                    placeholder="e.g., 'acute bronchitis' or 'fracture of tibia'"
                    class="w-full px-4 py-3 rounded-xl border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition duration-200"
                />
            </div>
            
            <!-- Search Results -->
            <div id="resultsContainer" class="max-h-96 overflow-y-auto pr-2">
                <div class="bg-gray-50 text-gray-400 text-sm p-4 rounded-xl text-center">
                    Start typing to see results.
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const searchInput = document.getElementById('searchInput');
            const resultsContainer = document.getElementById('resultsContainer');

            // Sample ICD-10-CM data.
            const icd10Data = [
                { code: 'J20.9', description: 'Acute bronchitis, unspecified' },
                { code: 'S82.209A', description: 'Unspecified fracture of shaft of unspecified tibia, initial encounter for closed fracture' },
                { code: 'M17.11', description: 'Unilateral primary osteoarthritis, right knee' },
                { code: 'E11.9', description: 'Type 2 diabetes mellitus without complications' },
                { code: 'I10', description: 'Essential (primary) hypertension' },
                { code: 'R51', description: 'Headache' },
                { code: 'K21.9', description: 'Gastro-esophageal reflux disease without esophagitis' },
                { code: 'L72.3', description: 'Sebaceous cyst' },
                { code: 'N18.9', description: 'Chronic kidney disease, unspecified' },
                { code: 'Z20.828', description: 'Contact with and (suspected) exposure to other viral communicable diseases' },
                { code: 'S06.0X0A', description: 'Concussion with loss of consciousness of up to 30 minutes, initial encounter' },
                { code: 'A09', description: 'Infectious gastroenteritis and colitis, unspecified' },
                { code: 'G43.909', description: 'Migraine, unspecified, not intractable, without status migrainosus' },
                { code: 'F33.1', description: 'Major depressive disorder, recurrent, moderate' },
                { code: 'J45.909', description: 'Unspecified asthma, uncomplicated' },
                { code: 'K59.00', description: 'Constipation, unspecified' },
            ];

            // render the results
            const renderResults = (results) => {
                resultsContainer.innerHTML = ''; // Clear previous results
                if (results.length === 0) {
                    resultsContainer.innerHTML = `<div class="bg-gray-50 text-gray-400 text-sm p-4 rounded-xl text-center">
                                                    No matching codes found.
                                                  </div>`;
                    return;
                }

                results.forEach(item => {
                    const resultItem = document.createElement('div');
                    resultItem.className = 'bg-white p-4 rounded-xl shadow-sm mb-2 border border-gray-200 hover:shadow-md transition-shadow duration-200 cursor-pointer';
                    
                    const codeElement = document.createElement('div');
                    codeElement.className = 'font-semibold text-lg text-blue-600';
                    codeElement.textContent = item.code;
                    
                    const descriptionElement = document.createElement('div');
                    descriptionElement.className = 'text-gray-700 text-sm';
                    descriptionElement.textContent = item.description;

                    resultItem.appendChild(codeElement);
                    resultItem.appendChild(descriptionElement);
                    resultsContainer.appendChild(resultItem);
                });
            };

            // Event listener for search input
            searchInput.addEventListener('input', (event) => {
                const query = event.target.value.toLowerCase().trim();
                
                if (query.length > 0) {
                    const filteredResults = icd10Data.filter(item => 
                        item.description.toLowerCase().includes(query)
                    );
                    renderResults(filteredResults);
                } else {
                    resultsContainer.innerHTML = `<div class="bg-gray-50 text-gray-400 text-sm p-4 rounded-xl text-center">
                                                    Start typing to see results.
                                                  </div>`;
                }
            });
        });
    </script>
</body>
</html>
