---
layout: page
icon: fas fa-search
order: 5
title: ICD-10 Search
---

<div class="bg-white rounded-2xl shadow-xl w-full max-w-2xl mx-auto overflow-hidden">
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

<script src="https://cdn.tailwindcss.com"></script>
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

<style>
    /* Ensure Tailwind styles work properly within the Jekyll theme */
    .bg-white { background-color: #ffffff !important; }
    .bg-gray-50 { background-color: #f9fafb !important; }
    .bg-gray-100 { background-color: #f3f4f6 !important; }
    .text-gray-400 { color: #9ca3af !important; }
    .text-gray-500 { color: #6b7280 !important; }
    .text-gray-700 { color: #374151 !important; }
    .text-gray-800 { color: #1f2937 !important; }
    .text-blue-600 { color: #2563eb !important; }
    .border-gray-200 { border-color: #e5e7eb !important; }
    .border-gray-300 { border-color: #d1d5db !important; }
    .rounded-xl { border-radius: 0.75rem !important; }
    .shadow-xl { box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04) !important; }
    .shadow-sm { box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05) !important; }
    .max-h-96 { max-height: 24rem !important; }
    .overflow-y-auto { overflow-y: auto !important; }
    .focus\:ring-2:focus { box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.5) !important; }
    .focus\:ring-blue-500:focus { --tw-ring-color: rgb(59 130 246 / 0.5) !important; }
    .transition-shadow { transition-property: box-shadow !important; transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1) !important; transition-duration: 150ms !important; }
    .duration-200 { transition-duration: 200ms !important; }
    .hover\:shadow-md:hover { box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06) !important; }
</style>