Aria Templates JSDeminifier
===========================

This repo is a fork of [Javascript Deminifier Firefox add-on](https://addons.mozilla.org/en-US/firefox/addon/javascript-deminifier/).
The only thing this adds on top of the original add-on is the **support for Aria Templates multipart files**.

If the AT multipart file (a proprietary format to carry JS and AT templates in one file) is served with the
HTTP response header typical JavaScript files (which is not recommended by the way), the JS parts of it will be split
and deminified properly, and TPL files will be left intact.

With the original extension, deminifying those files usually resulted in syntax errors -- since AT multiparts are not
valid JS files -- hence it was basically impossible to activate JSD on the websites using minified version of AT.

Since the add-on is configurable, you can also deminify AT multiparts which are served with different `Content-Type` (see below).

Installation, usage & Configuration
===================================

Uninstall JSDeminifier before you install ATJSD.

You may either use the files from the cloned repo (see "Hacking on this add-on" section) directly,
or create a ZIP and put it in your Firefox profile folder.

Once installed, there'll be a toggle button in your status bar (ATJSD ON / OFF), togglable per each tab.

The extension only runs for files that have HTTP `Content-Type` header matching
the values from `extensions.jsdeminifier.contenttypes` in `about:config`
(default is `text/javascript,application/javascript,application/x-javascript`).

Contributions
=============

Contributions are welcome. Note that any generic improvement proposals to JSD should be opened
[in the original repo](https://github.com/benmmurphy/jsdeminifier_xpi). Open issues and pull requests
to the current repo only it they concern Aria Templates files handling.

Hacking on this add-on
======================

1. Clone this repo (`git clone https://github.com/jakub-g/atjsd`) to a `C:\atjsd\` / `~/atjsd/` etc.
2. Locate your profile folder (open `about:support` page in Firefox, find **Profile Folder** -> **Show Folder** button).
3. In `$profileFolder/extensions/` folder, create a text file named `atjsd@ariatemplates.com`
and put there the path from step 1, with trailing slash, without trailing whitespace.
4. Run Firefox and confirm installation.

Changes you do in the add-on should be reflected instantly in the browser once you refresh the page.
Note that only files with certain HTTP response headers are minified. If your JS file is served as `text/plain`
(e.g. from `raw.github.com`), it won't be deminified.

For quick testing, you may e.g. create from command line a throwaway server (`localhost:8000`) in current folder with
`python -m SimpleHTTPServer` / `python -m http.server` (Python 2/3 respectively).

JSDeminifier original readme
============================

uses the javascript beautifier from jsbeautifier.org to beautify all http responses with the mime type text/javascript or application/javascript.

WARNING: this plugin is applied globally and may screw up your web browsing session.

KNOWN ISSUES
------------

* doesn't handle character encoding properly
* weird errors when calling 'this.originalListener.onStartRequest(request, context);'
