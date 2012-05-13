
# Connect Form

Connect Form is a multipart / urlencoded form parsing middleware utilizing [node-formidable](http://github.com/felixge/node-formidable) behind the scenes.

This module is now deprecated and will eventually be removed, Connect >= 1.8.0 `bodyParser()` supports multipart/form-data, populating `req.body` much like application/json. An alternative to the core's `bodyParser()` is [parted](https://github.com/visionmedia/parted).

<i><b>This module has indeed disappeared upstream.</b> This fork preserves it
since our app still relies on it. (We'll upgrade soon enough.)<i>

## Installation

via npm:

	$ npm install https://github.com/thingdom/connect-form/tarball/master

## Example

    var form = require('connect-form');
    var server = connect.createServer(
	    form({ keepExtensions: true }),
	    function(req, res, next){
		    // Form was submitted
	        if (req.form) {
		        // Do something when parsing is finished
		        // and respond, or respond immediately
		        // and work with the files.
	            req.form.complete(function(err, fields, files){
	                res.writeHead(200, {});
	                if (err) res.write(JSON.stringify(err.message));
	                res.write(JSON.stringify(fields));
	                res.write(JSON.stringify(files));
	                res.end();
	            });
	        // Regular request, pass to next middleware
	        } else {
	            next();
	        }
	    }
	);