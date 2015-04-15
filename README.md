# superagent-legacyIESupport

A plugin for the Superagent Javascript library to support cross domain requests on IE 8 &amp; 9.  Now on npm : https://www.npmjs.com/package/superagent-legacyiesupport.

## Description

Surprise surprise, CORS requests don't work quite the same way in IE 8 & 9 as they do in other browsers, and they come with some extra restrictions.  This is a nice page describing some of the finer details: http://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx.

In a nutshell, CORS is implemented with its own `XDomainRequest` object, seperate from `XMLHTTPRequest`.  As a bonus, it doesn't support sending cookies, at all, or custom headers, or any verbs other than GET and POST, and requests must be made to the same scheme as the current page.

Superagent out of the box does support making requests in IE 8 & 9 to origins on the same domain (which doesn't include sub domains by the way), and does support cross domain requests with CORS-supporting services on the other major browsers, including IE 10 & 11.

However, you'll need to do something similar to what this plugin does if you want to make cross domain requests on IE 8 & 9.

Also bear in mind, if you want to do any cross domain requests from any version of IE, your service will also need to supply a valid P3P header for IE to honour the response.

Have fun.

## Usage
```
var request = require('superagent'),
    legacyIESupport = require('./superagent-legacyIESupport');

request
   .get(...)
   .use(legacyIESupport)
   .withCredentials() // this will be ignored if on IE 8 & 9
   .end(...);
```
