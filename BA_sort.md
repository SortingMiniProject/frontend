---
layout: page
title: Sorting Mini Project
permalink: /sort/
---
<style>
    @import url("https://fonts.googleapis.com/css?family=Whisper");
    body {
        font-family: 'Arial', sans-serif;
        padding: 20px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 20px;
    }

    th, td {
        border: 1px solid #ddd;
        padding: 8px;
        text-align: left;
    }

    thead {
        background-color: #f2f2f2;
    }

    #title {
        font-size: 20px;
        font-weight: bold;
        margin-bottom: 10px;
    }

    label {
        margin-right: 10px;
    }

    button {
        margin-right: 10px;
        margin-top: 10px;
    }

    #page-number-input {
        margin-right: 10px;
    }

    #search-input {
        margin-right: 10px;
    }

    #time-taken {
        font-size: 16px;
        font-weight: bold;
        margin-top: 20px;
    }

    #body2 tr:nth-child(even) {
        background-color: #f9f9f9;
    }

    #body2 tr:hover {
        background-color: #f5f5f5;
    }
</style>
<head>
    <!-- <script src = "http://localhost:8085/api"></script> -->
</head>
<body>
    <!-- <label id="sort-type">Sort Type</label> -->
    <button class="Insertion Sort" id="insertion-button" style="height:20px;width:100px">Insertion Sort</button>
    <button class="Merge Sort" id="merge-button" style="height:20px;width:100px">Merge Sort</button>
    <button class="Selection Sort" id="selection-button" style="height:20px;width:150px">Selection Sort</button>
    <button class="Bubble Sort" id="bubble-button" style="height:20px;width:100px">Bubble Sort</button>
    <br><label id="time-taken">Complexity</label>
    <table id="table">
        <thead>
            <tr>
                <th colspan=2 id="title">Choose a sort type to start!</th>
            </tr>
        </thead>
        <tbody id="body">
            <tr>
                <td>City Number</td>
                <td>City Name</td>
            </tr>
        </tbody>
        <tbody id="body2">
        </tbody>
    </table>
    <!-- Pagination Controls -->
    <button id="prev-button" style="height:20px;width:100px">Previous</button>
    <button id="next-button" style="height:20px;width:100px">Next</button>
    <!-- Input box for page number -->
    <br><label for="page-number-input">Go to page:</label>
    <input type="number" id="page-number-input" style="width: 50px;" min="1">
    <button id="go-button" style="height:20px;width:60px">Go</button>
    <!-- Search box for city names -->
    <br><label for="search-input">Search City:</label>
    <input type="text" id="search-input" style="width: 150px;">
    <button id="search-button" style="height:20px;width:60px">Search</button>
    <button id="clear-search-button" style="height:20px;width:100px">Clear Search</button>
    <br><button class="Delete" id="delete-button" style="height:20px;width:100px">Reset Table</button>
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
                body2.appendChild(row);
            }
            // document.getElementById('sort-type').innerHTML = "Sort Type: " + currentSortType;
            document.getElementById('time-taken').innerHTML = "Complexity: " + currentSortTime + " seconds";
            document.getElementById('title').innerHTML = "147, 400 cities sorted by: " + currentSortType + " sort";
        }
        function resetTable() {
            const element = document.getElementById("body2");
            while (element.firstChild) {
                element.removeChild(element.firstChild);
            }
            document.getElementById('title').innerHTML = "Choose a sort type to start!";
            document.getElementById('time-taken').innerHTML = "Complexity";
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
                    body2.appendChild(row);
                }
                document.getElementById('title').innerHTML = "Search results for: " + searchQuery;
            } else {
                alert("No cities found with that name.");
                resetTable();
            }
        });
        document.getElementById('clear-search-button').addEventListener('click', () => {
            renderPage(currentPage);
        });
        function handleSort(sortType, baseUrl) {
            document.getElementById('title').innerHTML = "loading...";
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