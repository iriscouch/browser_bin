# Run an NPM command-line program in the browser

You have a useful program from an NPM package. But you want to run it from the browser.

Browser Bin will bundle that program into a web page and Javascript files that does the same thing. CommonJS code is wrapped in RequireJS, and there is a virtual terminal.

## Usage

I like to use [follow](https://github.com/iriscouch/follow) to watch my Couch database updates.

    $ env since=18 heartbeat=120s follow http://jhs.iriscouch.com/files
    Watching: http://jhs.iriscouch.com/files
    Database confirmed: http://jhs.iriscouch.com/files
    Streaming response:
    Change:{"seq":21,"id":"img","changes":[{"rev":"6-2b6f73ef4b52995776b8794a9930be2e"}]}
    Change:{"seq":23,"id":"cors","changes":[{"rev":"2-4875ebb0024826d2b85594aebf8c0c57"}]}
    Change:{"seq":26,"id":"foo","changes":[{"rev":"3-ed03b380f09120e7216011b32503effd"}]}
    Retry since 26 after 1000ms

To run Follow via browser Javascript and HTML, use browser_bin:

    $ git clone git://github.com/iriscouch/follow
    $ cd follow
    $ cat package.json # Looks like "cli.js" is the real "follow" command.
    $ browser_bin cli.js

You're done! Publish the static files on the web and visit `index.html`.

    $ cp -r browser_bin/ /var/www/

Now you can run Follow by [visiting its URL][demo]. URL query parameters are accessible in `process.env`.

[demo]: http://jhs.iriscouch.com/files/follow/follow.html

## Porting Notes

Browser Bin is not magic. It just makes a web page that loads everything into the browser correctly. If you do Node stuff like open a file, obviously that will not work.

Browser Bin provides workalikes for some of the Node library:

* events and `EventEmitter`
* util
* request via [request.jquery][req]

[req]: https://github.com/iriscouch/request_jquery
