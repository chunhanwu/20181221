# Javascript 同一tr裡多個td排序
<strong>初階概念<strong>
```
<!DOCTYPE html>
<html>
<body>
    <p>回答:Javascript 同一tr里多個td排序</p><br>
    <button onclick="sort()">排序</button>
    <p id="demo"></p>
    <script>
        //初始化:未整理資料
        var arr = ["b", "a", "d", "c"];
        document.getElementById("demo").innerHTML = arr;

        /*
        以下整理邏輯
          原理:使用array的sort方法
          然後拼接table字串
          在輸出到DOM裡面
        */
        function sort() {
            arr.sort();
            var str_html = '<table border=1><tr>';
            for (i = 0; i < arr.length; i++) {
                str_html += "<td>" + arr[i] + "</td>";
            }
            str_html += '</tr></table>';

            document.getElementById("demo").innerHTML = str_html;
        }
    </script>
</body>
</html>
```
<strong>進階概念<strong>
```
<!DOCTYPE html>
<html>

<body>
  <p>回答:Javascript 同一tr里多個td排序</p>
  <hr>
  <button onclick="sort()">排序</button><br>
  <hr>
  <table border=1>
    <tr>
      <td>b</td>
      <td>a</td>
      <td>d</td>
      <td>c</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>5</td>
      <td>1</td>
    </tr>
  </table>
  <hr>
  <table border=1>
    <tr>
      <td>g</td>
      <td>q</td>
      <td>z</td>
      <td>c</td>
    </tr>
    <tr>
      <td>22</td>
      <td>44</td>
      <td>552</td>
      <td>12</td>
    </tr>
  </table><br>
  <script>
    function sort() {
      //先挑出所有tr dom，並分組
      var trs = document.querySelectorAll("table tr");
      [].forEach.call(trs, function (tr) {
        //====排序====
        //抓取tr裡面的td dom
        var tds = tr.querySelectorAll("td");
        
        //這邊一定要另外用個字串集合盛裝，不然改值的時候，會有錯位修改DOM的情況
        var paraArr = [].slice.call(tds).sort(function (a, b) {
          return a.textContent > b.textContent ? 1 : -1;
        });
        
        //把td裡面的值抓出來得出一個字串集合
        var str_arrs = [];
        [].forEach.call(paraArr, function (td) {
          str_arrs.push(td.innerHTML);
        });

        //====把排序結果顯示到table裡面====
        var index = 0;
        [].forEach.call(tds, function (td) {
          td.innerHTML = str_arrs[index++];
        });
      });
    }
  </script>
</body>

</html>
```
