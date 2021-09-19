# athena-123
A website that lets you do simple commands with your voice. 
Idea from talater/annyang. Their github is https://github.com/TalAter/annyang.

## Introduction
I started off wanting to do a speech identification project, using an API to figure out how to combine that with facial recognition on Iphones. However, I soon realized it was a massive library that were too time consuming and were too out of my scope for my technical abilities for me to put on my own personal laptop, so I switched the project to a speech recognition website. Using web dev and design and using my own commands, I turned the website more into a personal "Siri". 

## Research
I first started with research different speech recognition APIs that I could implement on my laptop to run speech. I tried implementing Kaldi, alphacep, and even cmusphinx, but they were way to complicated to integrate onto my laptop. I then shifted my lens on a different project. The new project was using one of the APIs to have a speech recognition based website that will allow a user to run commands. Although the algorithm for the speech recognition software was already written, I still had to write my own code and commands to get the website to its final result. 



## Implementation
I have four commands, all within the index.html file. These are all written in Javascript, and to run these functions, you could clone the annyang repository and put these functions in the commadn section in the index.html. The first is the math command, the second is the weather and mapping function, the third is the jokes command, and the last is the timer. 
````html
var calculate = function(tag){
      if (re.test(tag)){
      scrollTo("#section_maths"); 
      var answer = eval(tag);
     document.getElementById("calculations").innerHTML= answer;
     $('#calculations').show(answer);
      }
    };
````
````html

    var showTPS = function(tag) {
      scrollTo("#section_weather");
      const apiKey = '594635a290e1406b25e0ba09a461d4d1';
      var url = 'http://api.openweathermap.org/data/2.5/weather?q='+tag+'&appid='+apiKey + '&units=imperial';
      var xmlhttp;
      if (window.XMLHttpRequest){
        xmlhttp = new XMLHttpRequest();
      }
      xmlhttp.open("GET", url, false, null, null);
      xmlhttp.send();
      var respondText = xmlhttp.responseText;
      var stringText; 
      stringText = JSON.stringify(respondText);
      var indexVal1 = stringText.indexOf("temp");
      var indexVal2 = stringText.indexOf("visibility")
      var finalString = stringText.substring(indexVal1, indexVal2)
      document.getElementById("cold").innerText = finalString;
      $('#cold').show(finalString);
    }
    
    var mapping = function(tag){
      var url2;
      var longitude;
      var longitudeIndex;
      var latitude;
      var latitudeIndex;
      const apiKey = '594635a290e1406b25e0ba09a461d4d1';
      var url = 'https://api.openweathermap.org/data/2.5/weather?q='+tag+'&appid='+apiKey + '&units=imperial';
      var xmlhttps;
      if (window.XMLHttpRequest){
        xmlhttps = new XMLHttpRequest();
      }
      xmlhttps.open("GET", url, false, null, null);
      xmlhttps.send();
      var respondText = xmlhttps.responseText;
      var stringText; 
      stringText = JSON.stringify(respondText);
      longitudeIndex = respondText.indexOf("lon");
      latitudeIndex = respondText.indexOf("lat");
      longitude = respondText.substring(longitudeIndex + 5, longitudeIndex + 10);
      latitude = respondText.substring(latitudeIndex + 5, latitudeIndex + 10);
      url2 = "https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d300338.3370245011!2d" + longitude+ "!3d" + latitude + "!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2sus!4v1628026288115!5m2!1sen!2sus";
      document.getElementById("myFrame").src = url2;
    }
````
````html
var timer = function(tag){
  var aOrAn = tag.split(" ")[0];
  var trueOutput = tag.split(" ")[1];
  var numb = trueOutput.split(" ")[0];
  var degree = trueOutput.split(" ")[1];  
  console.log(numb);
  console.log(Number(numb));
  if (tag.includes("second")){
    setTimeout(alertFunc, numb * 1000)
  }
  else if (tag.includes("minute")){
    if (numb == "one"){
      setTimeout(alertFunc, 60000);
    }
    else if (numb == "five"){
      setTimeout(alertFunc, 300000);
    }
    else {
      setTimeout(alertFunc, parseInt(numb) * 60000);
    }
 
  }
  else if (tag.includes("hour")){
    setTimeout(alertFunc, numb * 360000)
  } 
}
function alertFunc(){
  alert('Timer is done');
}
````
````html
const jokeText = document.querySelector('.joke-text');
var checkJokes = function(tag){
  if (tag == "a joke" || tag == "another joke"){
    getJoke();
  }
}
function getJoke() {
  fetch('https://icanhazdadjoke.com/', {
    headers: {
      'Accept': 'application/json'
    }
  }).then(function(response) {
    return response.json();
  }).then(function(data) {
    const joke = data.joke;
    document.getElementById("haha").innerHTML= joke;
     $('#haha').show(joke);
  })
}

````
## Trials 
Using the Talater/annyang API, I learned that if you inspect the live server and click on the console section, the site will tell you what you've said. For example, let's say the user states "What's two plus two?" The annyang API will have a few different results in the console section. This helped me tremendously as I did all of my commands, as I could see what the API would output as I said something. Also, when I used the WeatherMap API, I had to cut out a lot of the information, as I only cared about the temperature.

### Usage:
Using Athena is pretty simple, with a few steps. First is to git clone the Athena repository. Next is to download VS Code, and open the folder containing Athena. Then, download Live Server, and once that is done, you can open up the index.html with Live Server and you can see the site on a Chrome browser. 
