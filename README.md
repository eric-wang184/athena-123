# athena-123
A website that lets you do simple commands with your voice. 
Idea from talater/annyang. Their github is https://github.com/TalAter/annyang.

## Introduction
I started off wanting to do a speech identification project, using an API to figure out how to combine that with facial recognition on Iphones. However, I soon realized it was too complex to implement on my own personal laptop, so I switched the project to a speech recognition website. Using web dev and design and using my own commands, I turned the website more into a personal "Siri". 

## Research
I first started with research different speech recognition APIs that I could implement on my laptop to run speech. I tried implementing Kaldi, alphacep, and even cmusphinx, but they were way to complicated to integrate onto my laptop. I then shifted my lens on a different project. The new project was using one of the APIs to have a speech recognition based website that will allow a user to run commands. Although the algorithm for the speech recognition software was already written, I still had to write my own code and commands to get the website to its final result. 

## Implementation
Using the Talater/annyang API, I learned that if you inspect the live server and click on the console section, the site will tell you what you've said. For example, let's say the user states "What's two plus two?" The annyang API will have a few different results in the console section. This helped me tremendously as I did all of my commands. For example, I had to specify for the timer function that "Set a one minute timer", the "one" was referring to the number 1, not the word "one". I first did the math command, then the weather command, then the timer, and finally the joke function. With the weather command, it was tricky as I first had to find the right weather API to put into my code. Then, I had to write a another function just for the map and the zooming in. That took me approximately three weeks to do. The code that I wrote for the two function is down below. 

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

### Result:
The result is four different commands. One is a math command that can do arithmetic. Another is a weather command that allows the user to find the temperature of a city using weathermap API. The weather command also comes with a map that zooms in to the city that the user wants to find the temperature of. There's also a joke command, using a dad joke API. Lastly, there is a timer command that pops up a window when the time is over. 
