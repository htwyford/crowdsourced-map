# crowdsourced-map

`crowdsourced-map` ([Demo](https://htwyford.github.io/crowdsourced-map/index.html))
is a simple map application that allows anyone to add pins to a public map. 
There are no frameworks, packages, or servers involved.
It uses a Google Form as its backend, so you can host it anywhere you can host
a few HTML/CSS/JS files. You can even just .zip up the project and send it
to users.

The project was originally developed for a literacy non-profit that wanted to
allow read-a-thon participants to add the books they've been reading to a map,
based on the setting of the book. I've written a walkthrough below (coming soon!)
with that non-profit fundraiser in mind: **someone who doesn't code**, and would 
not be comfortable setting up a server to run the back-end for a similar application.
More advanced users might find the walkthrough a little slow-paced, but it'll
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
Coming soon! :)
