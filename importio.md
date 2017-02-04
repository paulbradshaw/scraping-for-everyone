# How to use Import.io to scrape webpages

[Import.io](https://www.import.io/) is a web-based scraping service which you can use to scrape websites. It has a number of useful features, particularly if you want to create live visualisation: for example, you can create an 'API' for any scraper, which means it can be connected to other things.

In this tutorial I'll cover a basic process for scraping a directory on a website - and then move on to how to scrape multiple pages linked from that.

First you will need to sign up on [Import.io's signup page](https://import.io/signup) - if you struggle to find it, scroll to the bottom of the homepage and look for 'signup'.

## Creating a basic scraper on Import.io

To begin creating a new scraper it's a good idea to start from the Import.io dashboard, at [dash.import.io](https://dash.import.io/) (you'll need to be logged in first).

Click on the **New Extractor** button on the left.

A box should appear asking you to type the URL of the page that you want to scrape. We're going to scrape the [StarNow model directory](https://www.starnow.co.uk/talent/uk/models/). At first, we can use that to say what is the most popular name among models, and where are most models based. But as we drill down in more detail we can look at things like the diversity of models and whether those with more castings share particular characteristics.

Paste that URL, then: `https://www.starnow.co.uk/talent/uk/models/`

After a few moments, it will show you the results of its attempt to scrape that page. In this case, it should grab: the name and location of the model, a headshot, their name (on its own), and their location (on its own). Note that all of these also have links, which is actually an extra bit of data as you'll see.

It doesn't always work so smoothly on other websites, but we'll come onto some techniques to tackle that later.

But because it's worked, you can now click **Save**. 

After a moment, you should be taken to the dashboard for that scraper. If you run it now, you will get the data for that page.

**Great! We now have data on 20 models! What next?**

Well, it would good to grab a few hundred so we can analyse more...

### Generating a list of URLs to scrape

On the scraper dashboard you can apply this scraper to *more than one* URL. There are three ways to do this:

* Manually type or paste URLs into the box
* Generate URLs
* Take URLs from another scraper ('extractor') - we'll do this later

Of course typing URLs isn't much fun, so I'm going to show you how to generate a list of URLs - and then scrape them.

Click on the button **Show URL Generator**

The first page of the directory has a URL like this: `starnow.co.uk/talent/uk/models`

However, when you get to the bottom of that, and click through to the next page, it looks like this:

`https://www.starnow.co.uk/talent/uk/models/?p=2`

Note the `?p=2` at the end of that URL. This means it is page 2.
