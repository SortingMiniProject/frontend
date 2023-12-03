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
            <!-- <tr>
                <td>List Number</td>
                <td>Song Name</td>
            </tr> -->
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
        function createTable() {
            // const tbl = document.createElement("table");
            const body = document.createElement("tbody");
            const firstRow = document.createElement("tr");
            const cellList = document.createElement("td");
            const cellTextList = document.createTextNode("List Number");
            cellList.appendChild(cellTextList);
            firstRow.appendChild(cellList);
            const cellSong = document.createElement("td");
            const cellTextSong = document.createTextNode("Song Name");
            cellSong.appendChild(cellTextSong);
            firstRow.appendChild(cellSong);
            document.getElementById("body").appendChild(firstRow);
            for (let i = 0; i < 4; i++) {
                const row = document.createElement("tr");
                const cell1 = document.createElement("td");
                const cellText1 = document.createTextNode(`${i}`);
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode("TBD");
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                document.getElementById("body").appendChild(row);
            }
            document.getElementById("table").appendChild(tblBody);
            // document.body.appendChild(tbl);
            // tbl.setAttribute("border", "2");
        }
        function resetTable() {
            document.getElementById("body").remove(); 
        }
        document.getElementById("insertion-button").onclick = function(){
            createTable();
            document.getElementById("sort-type").innerHTML = "Sort Type: Insertion Sort";
        }
        document.getElementById("delete-button").onclick = function(){
            resetTable();
            document.getElementById("sort-type").innerHTML = "Sort Type:";
        }
    </script>
</body>