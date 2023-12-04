---
layout: page
title: Sorting Mini Project
permalink: /sort/
---

<head>
<!-- <script src = "http://localhost:8085/api"></script> -->
</head>
<body>
    <table id=table>
        <thead>
        <tr>
            <th colspan=2>4 Types of Sorts</th>
        </tr>
        </thead>
        <tbody id=body>
            <tr>
                <td>List Number</td>
                <td>City Name</td>
            </tr>
        </tbody>
        <tbody id=body2>
        </tbody>
    </table>
    <button class="Insertion Sort" id="insertion-button" style="height:20px;width:100px">Insertion Sort</button>
    <button class="Merge Sort" id="merge-button" style="height:20px;width:100px">Merge Sort</button>
    <button class="Selection Sort" id="selection-button" style="height:20px;width:150px">Selection Sort</button>
    <button class="Bubble Sort" id="bubble-button" style="height:20px;width:100px">Bubble Sort<br></button>
    <button class="Delete" id="delete-button" style="height:20px;width:100px">Reset Table<br></button>
    <br><label id="sort-type">Sort Type: </label>
    <br><label id="complexity">Complexity: <br></label>
    <script>
        function createTable(data) {
            for (let i = 0; i < data.sortedCities.length; i++) {
                const row = document.createElement("tr");
                const cell1 = document.createElement("td");
                const cellText1 = document.createTextNode(`${i}`);
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode("TBD");
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                body2.appendChild(row);
            }
            document.getElementById("table").appendChild(body2);
        }
        const baseUrl = "http://localhost:8085/api/insertion";
        fetch (baseUrl, { method: 'GET'})
            .then(response => {
                if (!response.ok) {
                    console.log(response);
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then(data => {
                console.log(JSON.stringify(data));
            })
            .catch(error => {
                console.error('Error:', error);
             });
        function resetTable() {
            const element = document.getElementById("body2");
            while (element.firstChild) {
            element.removeChild(element.firstChild);
            }
        }
        document.getElementById("insertion-button").onclick = function(){
            // createTable(data);
            document.getElementById("sort-type").innerHTML = "Sort Type: Insertion Sort";
        }
        document.getElementById("merge-button").onclick = function(){
            createTable();
            document.getElementById("sort-type").innerHTML = "Sort Type: Merge Sort";
        }
        document.getElementById("selection-button").onclick = function(){
            createTable();
            document.getElementById("sort-type").innerHTML = "Sort Type: Selection Sort";
        }
        document.getElementById("bubble-button").onclick = function(){
            createTable();
            document.getElementById("sort-type").innerHTML = "Sort Type: Bubble Sort";
        }
        document.getElementById("delete-button").onclick = function(){
            resetTable();
            document.getElementById("sort-type").innerHTML = "Sort Type:";
        }
    </script>
</body>