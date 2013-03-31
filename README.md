LikeLines-Player
============

*Welcome to the new home for the LikeLines player component.*
*The original prototype is still available on the*
*[Knight-Mozilla repository](https://github.com/Knight-Mozilla/likelines-mojo).*

## Introduction
Conventional online video players do not make the inner structure of the 
video apparent, making it hard to jump straight to the interesting parts. 
LikeLines provides users with a navigable heat map of interesting regions 
for the videos they are watching. The novelty of LikeLines lies in its 
combination of content analysis and both explicit and implicit user 
interactions.

![LikeLines concept diagram](https://raw.github.com/ShinNoNoir/likelines-player/master/doc/diagram.png)

The LikeLines system is being developed in the 
[Delft Multimedia Information Retrieval Lab](http://dmirlab.tudelft.nl/) 
at the Delft University of Technology.

## Using LikeLines on your Web page
Using LikeLines on your Web page is quite easy.
First, the following libraries and files are needed:

 * jQuery >= 1.7.2
 * likelines.js
 * likelines.css

These need to be included in the `<head>` of your Web page.
For example:
```html
  <head>
  	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
  	<script src="/js/likelines.js"></script>
	<link rel="stylesheet" href="/css/likelines.css">
  </head>
```
Just make sure that jQuery is loaded *before* the LikeLines script is included.

Finally, put a `div` with an `id` in your Web page where you want the 
LikeLines player to appear and create a new `LikeLines.Player` object
in JavaScript like in the example below:
```html
  <div id="myFirstLikeLinesPlayer"></div>
  <script>
    player = new LikeLines.Player('myFirstLikeLinesPlayer', {
	  video: 'http://www.youtube.com/watch?v=wPTilA0XxYE',
	  backend: 'http://likelines-shinnonoir.dotcloud.com/'
    });
  </script>
```

The `LikeLines.Player` constructor requires to arguments:
 1. A `div` or its `id` in which the LikeLines player will be embedded. 
 2. A configuration object.

The configuration object requires at the minimum a `video` entry pointing
to the video that needs to be played and a `backend` entry pointing to an
existing LikeLines server.

Optional configuration parameters include:
 * `width` and `height` for the internal video player.
 * `onReady` callback that is called when the LikeLines player is fully loaded.


## Installing the LikeLines server
In case you want to run your own LikeLines backend server, you have two options.
You can either install the required software on your own machine or 
deploy it on the dotCloud application platform.

### On your own computer or server
#### Prerequisites
The LikeLines server requires Python 2.6 or 2.7 to run, which can be obtained 
from http://www.python.org/download/, and [MongoDB](http://www.mongodb.org/downloads)
for storage.

In addition to Python and MongoDB, the following Python packages are needed:
 * Flask
 * PyMongo
 * Flask-PyMongo

The simplest way of installing these packages is using `pip`. You can install
`pip` by first installing `easy_install` by following the instructions 
[listed on this page](https://pypi.python.org/pypi/setuptools).
You can then execute the following command in a terminal to obtain `pip`:
```sh
$ easy_install pip
```

The required Python packages can then be installed as follows:
```sh
$ pip install Flask
$ pip install PyMongo
$ pip install Flask-PyMongo
```
*Note: Windows users should follow PyMongo installation instructions*
*[listed here](http://api.mongodb.org/python/current/installation.html).*

#### Running the server
This section assumes you have downloaded the full LikeLines source code
via `git` or through the Github Web interface. Once downloaded and unpacked 
to a directory, the following two processes need to be started.

The first process to be started is a MongoDB server on the the default port. 
You can start the MongoDB server by simply executing `mongod` in a terminal:

```sh
$ mongod
```

The second process is the actual LikeLines backend server that will 
receive requests to store and aggregate user playback behaviour.
To start this process, go into the `server` subdirectory and run
the `LikeLines.server` Python module. The example below shows how
to run the LikeLines server on port 9090.

```sh
$ cd likelines_source/server
$ python -m LikeLines.server -p 9090
```



## Demo
Running the demo requires:

 * A HTML5-compatible browser supporting the Canvas element and JavaScript.
 * Internet access (for the YouTube API and jQuery library).
 * Python 2.6+ (for the backend reference implementation) 
   with the following packages:
     * Flask
     * PyMongo
     * Flask-PyMongo
 * MongoDB (for the backend).

You can download the code via `git` or through the Github web interface. 
Once downloaded and unpacked to a directory, three processes need to be 
started in order to run the demo. These three processes can best be run 
in separate terminals or screens.

The first process is starting a web server (or use an existing one) which 
will serve demo web page and the LikeLines JavaScript library. Note that 
you cannot simply open the web page locally (the browser would simply 
refuse to execute JavaScript in a local context):

```sh
$ cd likelines-player
$ python -m SimpleHTTPServer 8080
```

Next step is to make sure a MongoDB server is running on the default port. 
You can start the MongoDB server by simply executing `mongod`:

```sh
$ mongod
```

The final step is to run the backend server for LikeLines. This server will 
receive requests to store and aggregate user playback behaviour:

```sh
$ cd likelines-player/server
$ python -m LikeLines.server -p 9090
```

When the three processes are running, please point your browser to 
[http://localhost:8080/examples/demo.html](http://localhost:8080/examples/demo.html) 
to start the demo.

## Roadmap and plans
 * March 2013: Make LikeLines deployable on at least one cloud platform.
 * March 2013: Finalize support for content analysis indexing.
 * Future: Add HTML5 <video> support.
 * Future: Improve UI.
 * Future: Introduce a [SMILA](http://www.eclipse.org/smila/) component 
   that treats a LikeLines server as a data source for indexing purposes.


## Acknowledgments

![CUbRIK](http://www.cubrikproject.eu/templates/rt_tachyon_j15/images/logo/light/logo.png)
