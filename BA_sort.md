---
layout: page
title: Sorting Mini Project
permalink: /sort/
---
<head>
    <!-- <script src = "http://localhost:8085/api"></script> -->
</head>
<body>
    <label id="sort-type">Sort Type</label>
    <label id="time-taken">Time Taken</label>
    <table id="table">
        <thead>
            <tr>
                <th colspan=3>4 Types of Sorts</th>
            </tr>
        </thead>
        <tbody id="body">
            <tr>
                <td>City Number</td>
                <td>City Name</td>
                <td>Time Taken (seconds)</td>
            </tr>
        </tbody>
        <tbody id="body2">
        </tbody>
    </table>
    <button class="Insertion Sort" id="insertion-button" style="height:20px;width:100px">Insertion Sort</button>
    <button class="Merge Sort" id="merge-button" style="height:20px;width:100px">Merge Sort</button>
    <button class="Selection Sort" id="selection-button" style="height:20px;width:150px">Selection Sort</button>
    <button class="Bubble Sort" id="bubble-button" style="height:20px;width:100px">Bubble Sort</button>
    <button class="Delete" id="delete-button" style="height:20px;width:100px">Reset Table</button>
    <!-- Pagination Controls -->
    <button id="prev-button" style="height:20px;width:100px">Previous</button>
    <button id="next-button" style="height:20px;width:100px">Next</button>
    <!-- Input box for page number -->
    <label for="page-number-input">Go to page:</label>
    <input type="number" id="page-number-input" style="width: 50px;" min="1">
    <button id="go-button" style="height:20px;width:60px">Go</button>
    <!-- Search box for city names -->
    <label for="search-input">Search City:</label>
    <input type="text" id="search-input" style="width: 150px;">
    <button id="search-button" style="height:20px;width:60px">Search</button>
    <button id="clear-search-button" style="height:20px;width:100px">Clear Search</button>
    <script>
        let currentPage = 1;
        const itemsPerPage = 100;
        let totalData = [];
        let currentSortType = "";
        let currentSortTime = "";
        function renderPage(pageNumber) {
            resetTable();
            const startIndex = (pageNumber - 1) * itemsPerPage;
            const endIndex = Math.min(startIndex + itemsPerPage, totalData.length);
            for (let i = startIndex; i < endIndex; i++) {
                const row = document.createElement("tr");
                const cell1 = document.createElement("td");
                const cellText1 = document.createTextNode(i+1);
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode(totalData[i]);
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                const cell3 = document.createElement("td");
                const cellText3 = document.createTextNode(currentSortTime);
                cell3.appendChild(cellText3);
                row.appendChild(cell3);
                body2.appendChild(row);
            }
            document.getElementById('sort-type').innerHTML = "Sort Type: " + currentSortType;
            document.getElementById('time-taken').innerHTML = "Time Taken: " + currentSortTime;
        }
        function resetTable() {
            const element = document.getElementById("body2");
            while (element.firstChild) {
                element.removeChild(element.firstChild);
            }
        }
        document.getElementById('next-button').addEventListener('click', () => {
            if (currentPage * itemsPerPage < totalData.length) {
                currentPage++;
                renderPage(currentPage);
            }
        });
        document.getElementById('prev-button').addEventListener('click', () => {
            if (currentPage > 1) {
                currentPage--;
                renderPage(currentPage);
            }
        });
        document.getElementById('go-button').addEventListener('click', () => {
            const enteredPage = parseInt(document.getElementById('page-number-input').value);
            const maxPage = Math.ceil(totalData.length / itemsPerPage);
            if (!isNaN(enteredPage) && enteredPage >= 1 && enteredPage <= maxPage) {
                currentPage = enteredPage;
                renderPage(currentPage);
            } else {
                alert("Please enter a valid page number between 1 and " + maxPage);
            }
        });
        document.getElementById('search-button').addEventListener('click', () => {
            const searchQuery = document.getElementById('search-input').value.toLowerCase();
            const filteredData = totalData.filter(city => city.toLowerCase().includes(searchQuery));
            var searchData;
            currentPage = 1; // Reset to first page
            if (filteredData.length > 0) {
                searchData = filteredData; // Update the data to the filtered results
                resetTable();
                // const startIndex = (pageNumber - 1) * itemsPerPage;
                // const endIndex = Math.min(startIndex + itemsPerPage, totalData.length);
                for (let i = 0; i < searchData.length; i++) {
                    const row = document.createElement("tr");
                    const cell1 = document.createElement("td");
                    const cellText1 = document.createTextNode(i+1);
                    cell1.appendChild(cellText1);
                    row.appendChild(cell1);
                    const cell2 = document.createElement("td");
                    const cellText2 = document.createTextNode(searchData[i]);
                    cell2.appendChild(cellText2);
                    row.appendChild(cell2);
                    const cell3 = document.createElement("td");
                    const cellText3 = document.createTextNode(currentSortTime);
                    cell3.appendChild(cellText3);
                    row.appendChild(cell3);
                    body2.appendChild(row);
                }
            } else {
                alert("No cities found with that name.");
                resetTable();
            }
        });
        document.getElementById('clear-search-button').addEventListener('click', () => {
            handleSort(currentSortType, "http://localhost:8085/api/" + currentSortType.toLowerCase());
        });
        function handleSort(sortType, baseUrl) {
            fetch(baseUrl, { method: 'GET'})
                .then(response => response.json())
                .then(data => {
                    totalData = data.sortedCities;
                    currentSortType = sortType;
                    currentSortTime = data.timeInSeconds;
                    currentPage = 1;
                    renderPage(currentPage);
                })
                .catch(error => console.error('Error:', error));
        }
        document.getElementById("insertion-button").onclick = () => handleSort("Insertion", "http://localhost:8085/api/insertion");
        document.getElementById("merge-button").onclick = () => handleSort("Merge", "http://localhost:8085/api/merge");
        document.getElementById("selection-button").onclick = () => handleSort("Selection", "http://localhost:8085/api/selection");
        document.getElementById("bubble-button").onclick = () => handleSort("Bubble", "http://localhost:8085/api/bubble");
        document.getElementById("delete-button").onclick = resetTable;
    </script>
</body>