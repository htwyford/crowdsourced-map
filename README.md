# crowdsourced-map

`crowdsourced-map` ([Demo](https://htwyford.github.io/crowdsourced-map/index.html))
is a simple map application that allows anyone to add pins to a public map. 
There are no frameworks, packages, or servers involved.
It uses a Google Form as its backend, so you can host it anywhere you can host
a few HTML/CSS/JS files. You can even just .zip up the project and send it
to users.

The project was originally developed for a literacy non-profit that wanted to
readers to add their favourite books to a map, based on the book's setting.
I've written a walkthrough below with someone who works at that non-profit in 
mind: **someone who doesn't code**, and would not be comfortable setting up 
a server to run the back-end for a similar application.
More advanced users might find the walkthrough a little slow-paced, but it will
get you set up nonetheless.

`crowdsourced-map` is free under the MIT License, but Google requires that you
pay for the use of its Maps API. They offer $200 of free credit each month,
which should cover most use-cases for an application like this one. Be advised
Google requires that you provide a credit card to use this free credit. You can
set up and test `crowdsourced-map` without signing up for a Google Maps API key,
but you will need one by the time you publish the app.

> ### A note on scale
> Since `crowdsourced-map` doesn't use a typical backend, it is not possible
> to enforce any real security measures around data submission. 
> Only use `crowdsourced-map` in environments where you are expecting a small 
> audience, such as a local fundraising drive, personal project, or a school 
> assignment. Even after you take these precautions, an attacker can always 
> insert bad data due to the crowdsourced nature of the map. 
> Removing malicious entries is easy, but please be aware of the risk.

## Walkthrough
1. __Get a copy of `crowdsourced-map`__
If you're familar with Git, clone this repo.
If you're not, click _Clone or Download_, `Download ZIP`, then unzip the
downloaded file.
2. __Set up your Google Form__
To begin using `crowdsourced-map`, you need to set up the Google Form that will
serve as the back-end for the app. 
Create a new Google Form in Google Drive and add the fields you would like users
to be able to enter. The original `crowdsourced-map` allowed users to enter 
their own name, the name of a book they read, the author of that book, and
finally a "Location" field for the book's setting. You can pick whatever fields
suit your use case, but you must include "Location", "Latitude", and
"Longitude" fields.
`crowdsourced-map` is easiest to use if you pick three custom fields in
addition to the Location/Latitude/Longitude fields. With that said, you can use
any number of fields with some editing.
If you use a corporate Google account, make sure that your form can be filled 
by someone outside your organization. Do this by clicking the gear icon on the
Edit Form page and unchecking the appropriate box.
> ### Forget about how it looks!
> Don't worry about the Latitude/Longitude fields or how the Google Form looks;
> the user will never see them.

3. __Set up your Google Sheet__
Once your Google Form is complete, make sure it is sending its results to
a Google Sheet. You can find the Sheet by clicking on the _Responses_ tab of
the Edit Form page and clicking the green Sheets icon.
Once the Sheet is open, go to File > Publish to Web... and click Publish.
Close the Publish box and click the Share button at the top right. Turn
link sharing on, and make sure "Anyone with the link **can view**" is selected.
Make a note of the link and in particular the spreadsheet ID. The spreadsheet ID
is the long alphanumeric code betqween `/d/` and `/edit`. For instance, if your
sharable link is
https://docs.google.com/spreadsheets/d/1MkdonOT3oP4ofwgM_9DL3njkBNrcValWMt-X-WKveDI/edit?usp=sharing,
the spreadsheet ID is 1MkdonOT3oP4ofwgM_9DL3njkBNrcValWMt-X-WKveDI. 

In your copy of `crowdsourced-map`, add the spreadsheet ID to the 
`const spreadsheetID = ` line in `scripts/map.js`.

4. __Gather your Google Form data__
You will need to gather some data from your Google Form. Open your Form, and
enter your browser's developer tools. If you're not sure how to do this,
Google instructions for the browser you use.
Most modern developer tools place an icon that resembles a cursor entering a box
in the top-left corner of the window. Click that icon, and then click on one of
the text boxes on your Form. The developer tools will highlight the code behind 
that text box. Here is an example:
[img](docs/form_cursor_example.png)

In the line of code highlighted, make a note of the value for `name=`. In the 
screenshot above, it is `entry.870886307`. Repeat this for every input on 
the form.

Finally, search in the developer tools inspector for `/formResponse`. A URL will
be highlighted. Take a note of this URL.
[img](docs/form_response_example.png)

5. __Input your Form data into your website__
You will now use the data you gathered in step 4 to make `crowdsourced-map` come
to life. Open your copy of `index.html`. Make the following changes:
* On line 25, where the `<form>` element begins, replace the `action=` value with
the `/formResponse` URL you gathered in step 4.
* Following line 25 are small repeated blocks of code, wrapped in 
`<div class="book-input">` tags. Replace the `name=` value on the `<input>` tag
in the block with the corresponding `entry.XXXXXXXXX` value you grabbed in 
step 4. Take this take to update the text in the input's `<label>` as well.

At this point, you should have a __functioning application__. Just open the
`index.html` file in a web browser, and you should be able to add values to the
map. That said, some map features will be disabled since you have not yet gotten
permission (_an API key_) from Google to use the map.

6. __Acquire a Google Maps API key__
Follow step 1 of [Google's tutorial](https://developers.google.com/maps/documentation/javascript/get-api-key).
Once you have your API key