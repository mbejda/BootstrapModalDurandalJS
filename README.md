Bootstrap Modal Plugin for Durandal.js
========================


Bootstrap Modal Plugin For Durandal.js.

Tested on Bootstrap 3.2 and on Durandal 2.1.0.


## Installation

1. Add the BootstrapModal.js into Durandal.js plugins directory.
2. Activate the plugin.

``` javascript
    app.configurePlugins({
        router:true,
        dialog: true,
        bootstrapModal: true
    });
```

## API

##### dialog.showBootstrapDialog(obj, activationData)
Displays Twitter Bootstrap modal as a dialog.

##### dialog.showBootstrapMessage(message, title, options, autoclose, settings) 
Displays Twitter Bootstrap modal as a message..



## Example Usage

``` javascript 
define(['plugins/http', 'durandal/app', 'knockout', 'plugins/dialog'], function(http, app, ko,dialog) {
    return {
        displayName: 'Flickr',
        images: ko.observableArray([]),
        activate: function() {
            if (this.images().length > 0) {
                return;
            }
            var that = this;
            return http.jsonp('http://api.flickr.com/services/feeds/photos_public.gne', {
                tags: 'mount ranier',
                tagmode: 'any',
                format: 'json'
            }, 'jsoncallback').then(function(response) {
                that.images(response.items);
            });
        },
        select: function(item) {
            console.log('select')
            item.viewUrl = 'views/detail';

            dialog.showBootstrapModal(item, {});
        },
        canDeactivate: function() {
            return dialog.showBootstrapMessage('Are you sure you want to leave this page?', 'Navigate', ['Yes', 'No'], null);
        }
    };
});
```
