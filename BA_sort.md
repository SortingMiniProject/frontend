---
layout: page
title: Sorting Mini Project
permalink: /sort/
---

<head>
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
                <td>Song Name</td>
            </tr>
        </tbody>
    </table>
    <button class="Insertion Sort" id="insertion-button" style="height:20px;width:100px">Insertion Sort</button>
    <button class="Merge Sort" id="merge-button" style="height:20px;width:100px">Merge Sort</button>
    <button class="Selection Sort" id="selection-button" style="height:20px;width:150px">Selection Sort</button>
    <button class="Bubble Sort" id="bubble-button" style="height:20px;width:100px">Bubble Sort<br></button>
    <br><label id="sort-type">Sort Type: </label>
    <br><label id="complexity">Complexity: <br></label>
    <script>
        function createTable() {
            const tbl = document.createElement("table");
            const tblBody = document.createElement("tbody");
            for (let i = 0; i < 4; i++) {
                const row = document.createElement("tr");
                for (let j = 0; j < 2; j++) {
                    const cell = document.createElement("td");
                    const cellText = document.createTextNode(`${i}`);
                    cell.appendChild(cellText);
                    row.appendChild(cell);
                }
                document.getElementById("body").appendChild(row);
            }
            document.getElementById("table").appendChild(tblBody);
            // document.body.appendChild(tbl);
            // tbl.setAttribute("border", "2");
        }
        document.getElementById("insertion-button").onclick = function(){
            createTable();
            document.getElementById("sort-type").innerHTML = "Sort Type: Insertion Sort";
        }
    </script>
</body>