[<< home](https://gdavid04.github.io/ScratchExtensions/)
## HTTP requests

``` js
(function(ext) {
    ext._shutdown = function() {};

    ext._getStatus = function() {
        return {status: 2, msg: 'Ready'};
    };

    ext.getwebdataget = function(url, callback) {
        $.ajax({
              url: url,
              success: function( result ) {
                  callback(result);
              },
              error: function( xhr, ajaxOptions, thrownError) {
                 callback();
              }
        });
    };

    ext.webrequestget = function(url, callback) {
        $.ajax({
            url: url,
            success: function( result ) {
                callback();
            },
            error: function( xhr, ajaxOptions, thrownError) {
               callback();
            }
      });
    };

    ext.getwebdatapost = function(url, data, callback) {
        try {
        $.ajax({
              url: url,
              type: 'POST',
              data: JSON.parse(data),
              success: function( result ) {
                  callback(result);
              },
              error: function( xhr, ajaxOptions, thrownError) {
                 callback();
              }
        });
        } catch (e) {
            callback();
        }
    };

    ext.webrequestpost = function(url, data, callback) {
        try {
        $.ajax({
            url: url,
            type: 'POST',
            data: JSON.parse(data),
            success: function( result ) {
                callback();
            },
            error: function( xhr, ajaxOptions, thrownError) {
               callback();
            }
        });
        } catch (e) {
            callback();
        }
    };

    var descriptor = {
        blocks: [
            ['R', 'GET request to %s', 'getwebdataget', 'https://scratch.mit.edu'],
            ['w', 'GET request to %s', 'webrequestget', 'https://scratch.mit.edu'],
            ['R', 'POST request to %s with data %s', 'getwebdatapost', '', '{}'],
            ['w', 'POST request to %s wtih data %s', 'webrequestpost', '', '{}']
        ]
    };
    
    ScratchExtensions.register('HTTP requests', descriptor, ext);
})({});
```
