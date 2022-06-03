# catlily
This program utilized the free version of the https://thecatapi.com/.
The starting sample code is provided for free and does not need an API key.
The program was build in pure JavaScript and here is the backend code with comments.

````
//Create function ajax_get which takes a url and a callback function
function ajax_get(url, callback) {
    //Create the variable xmlhttp which equals a new XMLHttpRequest
    var xmlhttp = new XMLHttpRequest(); //An XMLHttpRequest is
    xmlhttp.onreadystatechange = function() { //xmlhttp.onreadystatechange is
      if (xmlhttp.readyState == 4 && xmlhttp.status == 200) { //xmlhttp.readystate //xmlhttp.status is
        console.log('responseText:' + xmlhttp.responseText); //xmlhttp.responseText is
        try {
          var data = JSON.parse(xmlhttp.responseText);
        } catch (err) {
          console.log(err.message + " in " + xmlhttp.responseText);
          return;
        }
        callback(data);
      }
    };
  
    //Create function xml.http which takes "GET", a url, and the true boolean
    xmlhttp.open("GET", url, true);
    xmlhttp.send();
  }

Click the 'Randomize' button to load a new cat image.
document.getElementById("randomize-button").addEventListener("click", function(e){
    e.preventDefault()
    ajax_get('https://api.thecatapi.com/v1/images/search?size=full', function(data) {
        //Get the first Array object of the JSON response
        var img = '<img src="' + data[0]["url"] + '">';
        document.getElementById("cats-image").innerHTML = img;
    });
});
````
