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

A box should now appear below, showing the URL that you pasted earlier to begin the scraper:

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/urlgenerator1.png)

The URL generator works by looking for patterns in URLs, such as page numbers, and then generating a list of URLs that follow that pattern, such as a collection of URLs which each ends in a different page number. 

But there's a problem with this URL: it doesn't have anything that we can use as a page number.

To solve this, we need to go back to the website and explore the results a bit further.

Start with the first page of the directory. Remember it has a URL like this: `starnow.co.uk/talent/uk/models`

However, when you get to the bottom of that, and click through to the next page, it looks like this:

`https://www.starnow.co.uk/talent/uk/models/?p=2`

Note the `?p=2` at the end of that URL. That is what we are looking for. We can test that this is a page numbering system by changing the `2` to a number `1`: this should take us back to the first page of results: 

`https://www.starnow.co.uk/talent/uk/models/?p=1`

And indeed, it does.

Now we can return to the URL generator in the scraper and **edit** the URL so that *now* it has a page number too:

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/editparameter.png)

When you click **OK** you should now see some new options. This is because the new URL has a *parameter* (the page number) that it can use to generate more URLs:

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/importiorange.png)

That *parameter* is highlighted in green: the number `1` has been replaced in the URL with `{parameter-1}`. That just tells you that Import.io has recognised that number as a *parameter* (just a fancy word for 'ingredient') that is being used to specify the page number.

Underneath, then, you can see more details about that parameter, which you can edit:

* **Range of numbers**: at the moment Import.io is assuming that this parameter refers to a range of numbers. But sometimes a parameter might be a *List of values* (like place names). You can specify that here if you need to. But in this case it's right.
* **1 to 100**: the next two boxes specify the range of values you want to generate URLs for. In this case we've put `1` and `100` as the start and end values. This means it will generate 100 URLs, each ending in a different number. 
* **step** is currently set to `1`. This means that it will count from 1 to 100 in *steps* of 1. If you changed *step* to `5` then it would count in steps of 5 (i.e. 1, 6, 11, and so on)
* **Number of generated URLs:** tells you how many have been generated. In this case, it's 100. Underneath, you can see that list of URLs.
* **Add to list**: if you're happy with those URLs, you can click this button to add them to the list that you're about to run the 'extractor' (scraper) on.

Click **Add to list**.

Now the URLs are added to the white box below. They are almost ready to be scraped - but first you need to do a couple of things.

* Check and remove duplicates
* Save the list
* Run URLs

At the top of your list is the original URL you first used: `https://www.starnow.co.uk/talent/uk/models/`

Remember that this is the *same* page as `https://www.starnow.co.uk/talent/uk/models/?p=1`, so you need to remove it. To do that, click on the URL, and delete it.

To make sure there are no other duplicates, click **Remove duplicate URLs**

Why are we doing this? Well, if one page gets scraped twice then that's going to be misleading in any results. If we're counting what name appears most, for example, then the 20 models on that page are going to have their name counted twice. Clean data is important.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/importio_URLs.png)

Next, click **Save**. 

Then, click **Run URLs**. The scraper that you created for the first page of results should now run on *all* those URLs. It may take a while!

*Make sure you have clicked **Add to list** and **Save** or your scraper won't work properly.*

Once it has run, you should be taken to the *Run history* view of your dashboard, which looks like this:

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/runhistory.png)

So far we haven't changed the name of the scraper, so now is a good time to do so. To do that just click on the name, and change it to something meaningful (this is important because we'll need to be able to find it by name later).

The *run history* view shows when the scraper was run, how many URLs it scraped, how long it took, and how many rows of data it generated (in the example above, 220 rows - 20 for each of the 11 pages). To the right are buttons to download the data, view a log (this shows any errors), or preview the data. 

If you want to, you can click the download button (circled above) to get the data. You can choose to download it as a **CSV** or a **JSON** format. If you want to analyse it in a spreadsheet choose **CSV** (the **JSON** format is normally used for data visualisation using JavaScript).

**Great! We now have data on 2000 models! What next?**

## How to grab data on individual pages linked from the directory

Well, having 2000 names and locations is nice - but the really interesting data is on each of the 2000 profile pages. This initial scraper *has* scraped the 2000 *links* to those pages. We can use those - but first, we need to create a new scraper for a profile page.

First, you need to find a URL to use for your scraper. Go back to the directory, then, and find a URL for one of the profiles - it will look something like `https://www.starnow.co.uk/sophieshallai`.

Copy that URL.

Now, go back to the Import.io dashboard, at [dash.import.io](https://dash.import.io/) and click on the **New Extractor** button to create a new scraper for this page. Paste the URL for the profile page.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/extractorprofile.png)

This time the scraper doesn't work very well first time: it grabs all the comments posted to the profile page. But we don't want that information. We're going to have to *customise* this scraper.

First, get rid of everything that it has automatically grabbed, by clicking the **Clear** button. 

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/clearfields.png)

As soon as you do that, you will be taken to the 'Website' view, and a new column will have been created.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/newcolumn.png)

Click on 'New column' (in the hovering box on the right) to give it a name to describe the data you're going to identify. Let's pick 'ethnicity'.

Now, scroll down the page to find the data you want to grab and put in this column. Notice that the 'ethnicity' column box stays on the right, howevering over the top of the website (you can click and drag on the four-way arrow to move this if it's in the way).

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/identifydata.png)

When you find the data, however over it. You should see a faint pink box appear to show you what information will be grabbed if you click.

In the case of ethnicity, for example, depending where you hover, it will grab:

* The word 'Ethnicity:'
* The words 'White/Caucasian'
* The words 'Ethnicity: White/Caucasian'

Clearly you don't want to just grab the word 'Ethnicity', but either of the other two will get you what you need. Click when the right information is highlighted. It should now be shown in the box to the right.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/ethnicitygrab.png)

That will get you one piece of data (you can check it by switching to the *Data* tab at the top, then switch back to the *Website* view).

To add more data, click on the pink **Add column +** button in the upper right corner. As before, you need to give this a name, then scroll down and click on the data you want to put in that column.

By repeating this process you can grab all the demographic details. (However, if you try to grab other details (like castings), it will stop working. You'll have to create a separate scraper if you want those.)

Once you're finished, click **Save**.

Now you'll be taken to the dashboard for that new extractor. As before, you can specify a list of URLs to apply this extractor to. However, this time instead of generating a list of URLs, you need to select **URLs from another Extractor**

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/urlsfromextractor.png)

Underneath a *Selected extractor* box should appear with the hint *Search for extractor by name or id...*. Start typing the name of the extractor that you made before (the one that grabs the pages listing all the models). If you can't remember what it's called, it should be listed in the left hand column which shows all your extractors.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/urllist.png)

Once you select that extractor, a dropdown list should appear for you to select which *column* from that extractor contains the URLs you want to apply *this* extractor to. (In other words, the column containing the URLs for the profile pages).

The dropdown list will *only* show columns containing URLs. In this example there will be 4 listed: one of them (*Headshotgrid image*) contains the image URLs but the other 3 all contain the same URL of the profile page. You can select any of those.

![](https://raw.githubusercontent.com/paulbradshaw/scraping-for-everyone/master/importio/urlcol.png)

Once you've selected that column, click on **Run URLs** towards the top of the page. It will now run your new profile extractor on *all* the URLs that were grabbed by your previous extractor. Once it's finished you can download and analyse as before.
