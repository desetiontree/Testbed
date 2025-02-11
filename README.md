# Context

This is repository contains a small Web component, built on top of the [lit.dev](https://lit.dev) library,
which is lacking styling and relies on mock data for the tournament information.

Please, fork the respository in your own account, commit and push your changes in your own repository,
and submit a pull request (PR) against this repository.

Once you have a copy of the repository on your own machine, you can:
- Run the webserver with Python and the command `python3 -m http.server 8080` or
- Run the webserver as a VSCode extension (Live Server or Live Preview)
- Launch a Web browser at the address `http://127.0.0.1:8080/demos/`, for example.
- Follow the link for the Tournament Card Demo

# Directions

The demo environment does not require any build process.

Some dependencies, like for the `lit` library and some MWC components,
are loaded automatically in Chrome via the mechanism `import-map` (only
Safari does not plan to support it...). Feel free to use the JSPM service
to add (or remove) some dependencies.

The images and icons you may use when styling the Tournament card can be
stored locally and part of your committed changes, or can load them from
remote source. Just be mindful of the weight of the image you might drag in
such a small component.

# Evaluation Steps

## Styling the Component

Here is the rendering we are looking for:

![Tournament cards side-by-side](expected-rendering.png)

In the screenshot from above, the entire background is blue.
Please leave the demo page background in the white color so 
we can identify what's part of the component, what is not.

The simplicity of the HTML and the efficiency of the CSS styling
will be evaluated.

Extra point: Have a CSS pseudo class to insert automatically the
coin image in front of any piece of content wrapped in a &lt;span/&gt; and
tagged with the CSS class name `in-game-money`.

## Loading Tournanment Data.

The code contains the definitions for two tournaments and their are
loaded synchronously into the code.

In the `/data` folder, there are 2 JSON files defining two tournaments
currently used for load tests. Note that the data are equivalent to a payload
produced by a REST API (except for the headers).

Have the piece of content loaded by each component in an asychronous way,
in the method `_fetchTournamentInformation()`. The loaded data should be used in
place of the hardcoded ones.

Extra: display a message while the data is loading—rely on `setTimeout()` to 
delay the function completion so the temporary message is breifly visible.

## Interaction with a Router

The component will be used in different context, sometimes our context, sometimes
the ones of a customer or an sponsor. The component cannot infern on its knowledge of
a context to trigger navigation to the Tournament Detail page...

Have the handler of the `Details` button emitting a message that a listener, a router
in our context, will capture and will force a page update to display the Tournament Details page.

## Description of the Tournament back-end service

Please describe how you would host a service that will serve the JSON payloads as stored
in the `/data` folder. Ideally, the service relies on resources in the Cloud, for the runtime
and for the persistence layer.

Explain two or three strategies, present the pros and cons, and justify your choice.

In this exercise, there's really not totally right or totally wrong answers. The goal
is to see how you organize your arguments, how you rely on your experience, how up-to-date
you are with modern services.

Thanks a lot for giving a try. Good luck ;)

Regards, Dom

## Answer about Description of the Tournament back-end service

1. I highly recommend using socket services to implement the features. we can keep the up-to-date needs data and it will be updated on the client-side whatever its related data is changed.

2. we can choose a very standard communication way between the server and client-side. I mean, if those data will not be needed to update often, we don't need to send the requests to get the latest data to the server by using API. Whenever the user visits this page, we can get the necessary data using API ( fetch or axios or something )

3. we can make the perioded requests by the client-side to get the updated information but we need to make sure that it should be set up as well to let the server not down or very low performance.
I don't recommend its way however we might choose it according to the specifications.

I am a strong believer that any kind of web service and infrastructure must be depended on the specifications. There are lots of things to be considered between large-scale services and medium or small applications such as worth, cost vs profit, performance, maintenance, etc.

Above, I noted 3 options for your questions. I think we have to combine option1 and option2 because some of them need to be kept up-to-date information while it runs but other things might not need it. I think to do it according to the spec and performance would be great.

Thanks.
Bryan.
