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

This code runs fine. So let's move on and add and then run the next section:
* Convert the `xmldata` variable to an lxml object
* Use the `list` method ([explained here](https://www.tutorialspoint.com/python/list_list.htm)) to turn that lxml obect into a list
* Print the page number attributes from that list

```python
root = lxml.etree.fromstring(xmldata)
pages = list(root)

print "The pages are numbered:", [ page.attrib.get("number")  for page in pages ]
```

This also runs fine. Next, then:

* Loop through the first 100 items in a list and print the attribute of each element if it has the tag 'text'

```python
for el in list(page)[:100]:
    if el.tag == "text":
        print el.attrib
```

This works.
