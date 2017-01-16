## Scraping PDFs part 2

To identify the code surrounding the parts of the PDF we want to grab:

```xml
<text top="292" left="106" width="154" height="21" font="2">L. Campbell-Savours </text>
 <text top="313" left="106" width="151" height="21" font="2">L. Cope of Berkeley </text>
 <text top="334" left="106" width="172" height="21" font="2">B. D’Souza (Chairman) </text>
 ```

## Troubleshooting

We can start exploring and trouble-shooting our copied code by running it bit by bit. Start, for example, with the first part of the code which:

* Imports the libraries, 
* Specifies a URL (changed from the one in the original code)
* Reads the file at that URL,
* And prints the first 5000 characters (changed from 2000 in the original code)

```python
import scraperwiki
import urllib2
import lxml.etree

url = "https://www.parliament.uk/documents/lords-committees/house/Minutes/2016-17/HCMinutes-1-290616.pdf"
pdfdata = urllib2.urlopen(url).read()
print "The pdf file has %d bytes" % len(pdfdata)

xmldata = scraperwiki.pdftoxml(pdfdata)
print "After converting to xml it has %d bytes" % len(xmldata)
print "The first 5000 characters are: ", xmldata[:5000]
```

This code runs fine on Morph.io\*. So let's move on and add and then run the next section:
* Convert the `xmldata` variable to an lxml object
* Use the `list` method ([explained here](https://www.tutorialspoint.com/python/list_list.htm)) to turn that lxml obect into a list
* Print the page number attributes from that list (each object in the list is called 'page' - this is then used again later)

```python
root = lxml.etree.fromstring(xmldata)
pages = list(root)

print "The pages are numbered:", [ page.attrib.get("number")  for page in pages ]
```

This also runs fine. Next, then:

* Loop through the first 100 items in a list and print the attribute of each 'page' object element if it has the tag 'text'

```python
for el in list(page)[:100]:
    if el.tag == "text":
        print el.attrib
```

This works.

## Now the problematic bit

The next section of code defines a new function, and then the final part *runs* that function. Here's the first part:

```python
# this function has to work recursively because we might have "<b>Part1 <i>part 2</i></b>"
def gettext_with_bi_tags(el):
    res = [ ]
    if el.text:
        res.append(el.text)
    for lel in el:
        res.append("<%s>" % lel.tag)
        res.append(gettext_with_bi_tags(lel))
        res.append("</%s>" % lel.tag)
        if el.tail:
            res.append(el.tail)
    return "".join(res)
```

And here's the second part:

```python
# print the first hundred text elements from the first page
page0 = pages[0]
for el in list(page)[:100]:
    if el.tag == "text":
        print el.attrib, gettext_with_bi_tags(el)
```

The error that we get (in Morph.io at least) is: `UnicodeEncodeError: 'ascii' codec can't encode character u'\u2013' in position 7: ordinal not in range(128)`

As always, let's Google for some solutions.

For the Morph.io error there's [a thread on Stack Overflow here](https://stackoverflow.com/questions/5141559/unicodeencodeerror-ascii-codec-cant-encode-character-u-xef-in-position-0)

And the specific code suggested is this: `.encode('ascii', 'ignore')`

Here's that piece of code added to our print command:

```python
for el in list(page)[:100]:
    if el.tag == "text":
        print el.attrib, gettext_with_bi_tags(el).encode('ascii', 'ignore')
```

## Saving some data

Now let's add some code to save the data. First, we need a variable which will serve as an *index* for our entries. A simple way to do this is to create a variable set at zero and then add 1 to it every time the loop runs. That's the first line below:


```python
ID = 0
page0 = pages[0]
for el in list(page)[:100]:
    if el.tag == "text":
        print el.attrib, gettext_with_bi_tags(el).encode('ascii', 'ignore')
        record = {}
        record["text"] = gettext_with_bi_tags(el).encode('ascii', 'ignore')
        ID = ID+1
        record["ID"] = ID
        scraperwiki.sqlite.save(["ID"],record)
        print record
```

...after that line are the ones we already had. Then we create an empty dictionary variable with `record = {}` and store data in that in the lines that follow, before saving and printing it.

## Checking the data

We can see 28 rows have been stored, some of them empty. Comparing those to the original document, we might notice that all of the data comes from the *second* page of the document. 

So let's change one of the lines slightly to specify that we want to grab the first page:

```python
page0 = pages[0]
# In the original code, this said (page) but we've now changed it to (page0) which, in the line above, has been set to the first item in the pages variable
for el in list(page0)[:100]:
```

When we run the code this time, we now get the results from the first page. Curiously we also get the second page now. 

## Notes

\* *In QuickCode however, this generates an error: `ValueError`: specifically something about `Unicode strings with encoding declaration are not supported`. You'll [find some guidance about this error on the lxml documentation](http://lxml.de/parsing.html)*
