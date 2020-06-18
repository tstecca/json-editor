## json-editor

This repo tests a bug where the JSON Editor (https://github.com/json-editor/json-editor) slows down when the Google Chrome developer tools panel is open. In particular, the editor slows down when seeding the editor with a start value.  For comparision, this slow-down doesn't exist in Firefox when the dev tools are open, or at least it's not perceptible.

#### Startup

* Run `npm install`.  This install one package: http-server.  This lets you view the page.
* Run `npm run serve`. This starts the server.
* In Google Chrome, navigate to the address provided in the terminal by http-server.

#### The JSON Editor
All the markup and logic for this simple test is provided in the index.html file. There is a `<script>` tag in the page with just enought javascript to fetch a schema and data file and mount the editor with a `startval`.  There is a bit of logic to display the length of time from invoking the JSONEditor contructor to when the editor instance fires the ready event.

#### Steps to reproduce
* Open the index page in Chrome.  On first run it's a little slow because it has to fetch the schemas and json data.  Probably about 5000ms
* Refresh the page. All files are cached and it takes about 3500ms to be ready.
* Press f12 and wait for the dev tools to open.  Refresh the page. It should take about 12000ms for the ready event to file.
* Note that the editor is also logging out `-->` sings.

#### Notes
* I tested this issue with various versions of the editor and it is present in all the versions I tested. I even tested the original J. Dorn library.

#### Impact
This slow performance with the console open slows developers down when they have the console open.

#### Hopeful Resolution
* Opening the console would not affect the speed at which the editor performs.
* The `-->` logs would not show up.


