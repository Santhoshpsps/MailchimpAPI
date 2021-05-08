# MailchimpAPI


# node-mailchimp

A node.js wrapper for the MailChimp API.

_node-mailchimp_ exposes the following features of the MailChimp API to your node.js application:

 * MailChimp API (Versions 2.0, 1.3, 1.2 and 1.1)
 * MailChimp Export API (Version 1.0)
 * MailChimp Webhooks
 * MailChimp OAuth2 authorization
 * MailChimp Partner API (Version 1.3)
 * Mandrill API (Version 1.0)

Further information on the MailChimp API and its features is available at [http://apidocs.mailchimp.com](http://apidocs.mailchimp.com). If you want to know more about the Mandrill API and its features have a look at [https://mandrillapp.com/api/docs/](https://mandrillapp.com/api/docs/).


## Installation

Installing using npm (node package manager):

    npm install mailchimp

If you don't have npm installed or don't want to use it:

    cd ~/.node_libraries
    git clone git://github.com/gomfunkel/node-mailchimp.git mailchimp

Please note that parts of _node-mailchimp_ depend on [request](http://github.com/mikeal/request) by [Mikeal Rogers](http://github.com/mikeal). This library needs to be installed for the API and Export API to work. Additionally [node-querystring](http://github.com/visionmedia/node-querystring) is needed for the Webhooks to work. If you are using npm all dependencies should be automagically resolved for you.

## Usage

Information on how to use the MailChimp APIs can be found below. Further information on the API methods available can be found at [http://apidocs.mailchimp.com](http://apidocs.mailchimp.com). You can also find further information on how to obtain an API key, how to set up Webhooks and/or OAuth2 in your MailChimp account and much more on the MailChimp API pages.

Some methods of the MailChimp API take associative arrays as a parameter, for example the parameter `merge_vars` of the [`listSubscribe`](http://apidocs.mailchimp.com/api/1.3/listsubscribe.func.php) method. As there are no associative arrays in JavaScript you simply use an object with its properties being the keys, like in the following example:

```javascript
var merge_vars = {
	EMAIL: '/* E-MAIL ADDRESS */',
	FNAME: '/* FIRST NAME */',
	LNAME: '/* LAST NAME */'
};
```

### MailChimp API (when using MailChimp API version 2.0)

__Attention__: Support for v2.0 of the MailChimp API is not yet well tested. Please use with caution. When in doubt, stick to older versions of the API (v1.x) and skip to the next chapter for documentation.

_MailChimpAPI_ takes two arguments. The first argument is your API key, which you can find in your MailChimp Account. The second argument is an options object which can contain the following options:

 * `version` The API version to use (1.1, 1.2, 1.3 or 2.0). Defaults to 1.3. Make sure to explicitly use 2.0 here or refer to the next chapter for documentation on older API versions.
 * `userAgent` Custom User-Agent description to use in the request header.

All of the API categories and methods described in the MailChimp API v2.0 Documentation ([http://apidocs.mailchimp.com/api/2.0](http://apidocs.mailchimp.com/api/2.0) are available in this wrapper. To use them the method `call` is used which takes four parameters:

The callback function for each API method gets two arguments. The first one is an error object which is null when no error occured, the second one an object with all information retrieved as long as no error occured.

Example:

```javascript
var MailChimpExportAPI = require('mailchimp').MailChimpExportAPI;

var apiKey = 'Your MailChimp API Key';

try {
    var exportApi = new MailChimpExportAPI(apiKey, { version : '1.0', secure: false });
} catch (error) {
    console.log(error.message);
}

exportApi.list({ id : '/* LIST ID */'  }, function (error, data) {
    if (error)
        console.log(error.message);
    else
        console.log(JSON.stringify(data)); // Do something with your data!
});

Web App: https://rocky-ravine-74918.herokuapp.com/
