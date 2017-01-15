## Scraping PDFs part 2

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


* In QuickCode however, this generates an error: `ValueError`: specifically something about `Unicode strings with encoding declaration are not supported`. You'll [find some guidance about this error on the lxml documentation](http://lxml.de/parsing.html)
