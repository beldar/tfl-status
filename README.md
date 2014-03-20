# TFL Status Component
-------

This is a Web Component that uses [Polymer](http://www.polymer-project.org/) to create it and to provide a fallback in case the browser doesn't suppoer web components.

It provides a component that fetches the Tube Status updates with everything necessary encapsulated on one place.

It uses a YQL url to fetch the data XML, so it can be real time fetched with javascript.

You can find a working demo here: http://beldar.github.io/tfl-status/

To know more about web components [there](http://www.html5rocks.com/en/tutorials/webcomponents/customelements/) [are](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/) [tons](http://css-tricks.com/modular-future-web-components/) of [resources](https://www.google.co.uk/search?q=web+components) available.


# Installation

Dependencies
------------

You have to have installed [bower](http://bower.io/), and [compass](http://compass-style.org/install/). To install the first two you'll need [node](http://nodejs.org/) too.

Install
-------

Once you have all those and cloned the repo, go to the root of the project and run:

    bower install
    
That will download all the js and css dependencies of the project.

Then run:

    npm install
    
This will download all the node dependencies (including grunt)

Finally you can launch the demo running:

    grunt serve
    
You can build the project ready for production like this:

    grunt build
    
That will leave everything ready on the `/dist` folder

# How to use

There's an example/demo on the index.html of this project, but basically, you first need to include the platform.js:

    <script src="bower_components/platform/platform.js"></script>
    
Then, just below import the html of the element:

    <link rel="import" href="elements/tfl-status.html">
    
And finally place the element where you want it using the attributes that you need:

    <polymer-tfl-status refresh="5000" url="LineStatus.xml"></polymer-tfl-status>
    
The refresh attribute defines how often the element should refresh the data feed in miliseconds. 

You can also define a with and height:

    <polymer-tfl-status refresh="5000" width="300px" height="500px"></polymer-tfl-status>
    
Attributes summary
-----------

| Attribute | Functionality                        | Default        |
|-----------|--------------------------------------|----------------|
| refresh   | Defines the rate of the data refresh | 3000ms         |
| width     | Defines the component width          | 100%           |
| height    | Defines the component height         | auto           |

Events and API
------------
The components fires an event called `line-clicked` when the user clicks a Tube line and returns the data from the line, there's an example of how to use this on the index.html, which is:

    <script>
        document.addEventListener('WebComponentsReady', function() {
            var el = document.getElementsByTagName('polymer-tfl-status')[0];
            el.addEventListener('line-clicked', function(e){
                console.log(e.type, e.detail.line);
            });
        });
    </script>
    
For now the element has only one method api which is `stop()` that stops the refreshing of the component and it stops requesting for more data:

    var el = document.getElementsByTagName('polymer-tfl-status')[0];
    el.stop();