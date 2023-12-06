---
layout: page
title: Sorting Mini Project
permalink: /sort/
---

<head>
    <!-- <script src = "http://localhost:8085/api"></script> -->
</head>
<body>
    <table id="table">
        <thead>
            <tr>
                <th colspan=3>4 Types of Sorts</th>
            </tr>
        </thead>
        <tbody id="body">
            <tr>
                <td>Number of Cities Sorted</td>
                <td>Algorithm</td>
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
    <!-- Pagination buttons -->
    <button id="prev-button" style="height:20px;width:100px">Previous</button>
    <button id="next-button" style="height:20px;width:100px">Next</button>
    <!-- <br><label id="sort-type">Sort Type: </label>
    <br><label id="complexity">Complexity: <br></label> -->
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
                const cellText1 = document.createTextNode(totalData[i]);
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode(currentSortType);
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                const cell3 = document.createElement("td");
                const cellText3 = document.createTextNode(currentSortTime);
                cell3.appendChild(cellText3);
                row.appendChild(cell3);
                body2.appendChild(row);
            }
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
