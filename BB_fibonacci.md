---
layout: page
title: Fibonacci
permalink: /fibo/
---

<head></head>
<body>
    <input type="text" id="list-len" placeholder="Input a number">
    <button class="Go" id="fibo-button" style="height:20px;width:100px">Go!</button>
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
            <tr>
                <td id=method>Awaiting Input</td>
                <td id=complexity>Awaiting Input</td>
                <td id=length>Awaiting Input</td>
                <td id=fiboList>[]</td>
            </tr>
        </tbody>
    </table>
    <script>
        function go() {
            var fiboList = [];
            fiboList.push(1);
            fiboList.push(1);
            var fiboLen = document.getElementById("list-len").value;
            document.getElementById("method").innerHTML = "Method 1";
            document.getElementById("complexity").innerHTML = "TBD";
            document.getElementById("length").innerHTML = fiboLen;
            document.getElementById("fiboList").innerHTML = "[" + fiboList + "]";
        }
        document.getElementById("fibo-button").onclick = function(){
            go();
        }
    </script>
</body>