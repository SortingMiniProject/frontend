---
layout: page
title: Fibonacci
permalink: /fibo/
---

<head></head>
<body>
    <input type="text" id="list-len" placeholder="Input a number">
    <button class="Go" id="fibo-button" style="height:20px;width:100px">Go!</button>
    <button class="Delete" id="delete-button" style="height:20px;width:100px">Reset Table</button>
    <table>
        <thead>
        <tr>
            <th colspan=4>The Fibonacci Sequence</th>
        </tr>
        </thead>
        <tbody>
            <tr>
                <td>Method</td>
                <td>Complexity</td>
                <td>Length of List</td>
                <td>List</td>
            </tr>
        </tbody>
        <tbody id=body2>
        </tbody>
    </table>
    <script>
        function go() {
            var fiboList = [];
            fiboList.push(1);
            fiboList.push(1);
            var fiboLen = document.getElementById("list-len").value;
            for (let i = 0; i < 4; i++) {
                const row = document.createElement("tr");
                const cell1 = document.createElement("td");
                var methodNum = i + 1;
                const cellText1 = document.createTextNode("Method " + methodNum);
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode("TBD");
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                const cell3 = document.createElement("td");
                const cellText3 = document.createTextNode(fiboLen);
                cell3.appendChild(cellText3);
                row.appendChild(cell3);
                const cell4 = document.createElement("td");
                const cellText4 = document.createTextNode("[" + fiboList + "]");
                cell4.appendChild(cellText4);
                row.appendChild(cell4);
                body2.appendChild(row);
            }
        }
        function resetTable() {
            const element = document.getElementById("body2");
            while (element.firstChild) {
            element.removeChild(element.firstChild);
            }
        }
        document.getElementById("fibo-button").onclick = function(){
            go();
        }
        document.getElementById("delete-button").onclick = function(){
            resetTable();
        }
    </script>
</body>