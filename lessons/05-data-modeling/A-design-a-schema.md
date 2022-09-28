---
description: "How to design a schema using a design"
---

We're not building a UI for this API in this course, but, having a UI design is helpful when dsigning your models. Knowing what data needs to be in a UI gives you hints on what data needs to be recording in a DB.
<br>

We'll be using the design [here](https://www.framer.com/templates/chronos/) as are imaginary ChangeLog app. Let's observe this UI and figure out what resources we need to record in our DB.

<br>
So it looks like we'll need at least the following:
* `Update` - title, body, asset, status (in progress, launched), created at, version
* `Update Point` - belongs to an update, type (feature, improvement, bug), 
* `Feature`
<br>
And of course standard things like users. There will probably be supporting models that we create to help with querying and other logic like auth.
