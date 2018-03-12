# CapitalOneEmergencyCalls
```html
<html>
      <head>
        <script>

          var fileName = "SFData.csv";
          var data = "";

          req = new XMLHttpRequest();
          req.open("GET", fileName, false);

          req.addEventListener("readystatechange", function (e) {
            data = req.responseText ;
          });

          req.send();

          function getInfoByCode(c){
            if( data == "" ){
              return 'DataNotReady' ;
            } else {
              var rx = new RegExp( "^(" + c + ")\\s+\\|\\s+(.+)\\s+\\|\\s+\\s+(.+)\\|", 'm' ) ;

              var values = data.match(rx,'m');
              return { airport:values[2] , city:values[3] };
            }
          }

          function clickButton(){
            var e = document.getElementById("code");
            var ret = getInfoByCode(e.value);

            var res = document.getElementById("res");

            res.innerText = "Airport:" + ret.airport + " in " + ret.city;

          }

        </script>
       </head>
       <body>
        <input id="code" value="AUA">
        <button onclick="clickButton();">Find</button>
        <div id="res">
        </div>

       </body>
    </html>
  
