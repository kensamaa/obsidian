## MONOLITHS AND DECOUPLING

"Architecture" in software can mean _many_ different things, but in this lesson, we're talking about the high-level architecture of a web application from a structural standpoint. More specifically, we are concerned with the separation (or lack thereof) between the back-end and the front-end.

When we talk about "coupling" in this context, we're talking about the coupling between the _data_ and the _presentation logic_ of that data. Loosely speaking, when I say "a tightly coupled front-end and back-end", what I mean is:

### FRONT-END: THE PRESENTATION LOGIC

If it's a web app, then this is the HTML, CSS, and JavaScript that is served to the browser which will then be used to render any dynamic data. If it's a mobile app, then this is the compiled code that is downloaded on the mobile device.

### BACK-END: RAW DATA

For an app like YouTube, this would be videos and comments. For an app like Twitter, this might be tweets and users data. You can't embed the YouTube videos directly into the Youtube app, because a user's feed changes each time they open the app. The app downloads new raw data from Google's back-end each time the app is opened.

### MONOLITHIC

![monolith](https://i.imgur.com/ek42mUQ.png)

A monolith is a single, large program that contains all of the functionality for both the front-end and the back-end of an application. It's a common architecture for web applications, and it's what we're building here in this course.

Sometimes monoliths host a REST API for raw data (like JSON data) within a subpath, like `/api` as shown in the image. That said, there are even more tightly coupled kinds of monoliths that inject the dynamic data directly into the HTML as well. The nice thing about separate data endpoints is that they can be consumed by any client, (like a mobile app) and not just the website. That said, injection is typically more performant, so it's a trade-off. WordPress and other web_site_ builders typically work this way.

### DECOUPLED

![decoupled](https://i.imgur.com/VDJk0zU.png)

A "decoupled" architecture is one where the front-end and back-end are separated into different codebases. For example, the front-end might be hosted by a static file server on one domain, and the back-end might be hosted on a subdomain by a different server.

Depending on whether or not a load balancer is sitting in front of a decoupled architecture or not, the API server might be hosted on a separate domain (as shown in the image) _or_ on a subpath, as shown in the monolithic architecture. A decoupled architecture allows for either approach.