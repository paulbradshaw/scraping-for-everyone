# Introduction

![](images/torchrelayheadlines400.png)

In May 2012 I was sat in the cafe of the Museum of Science and Industry in Manchester, England, clicking through webpages on my laptop. It was the first day of the Olympic Torch Relay, and I had been invited to contribute to a citizen journalism project called [#Media2012](https://www.journalism.co.uk/news-features/media2012-olympics-citizen-journalism-newswire/s5/a548988/).

As I moved from section to section on the official London 2012 website, one page in particular caught my attention: it contained links to the stories of thousands of official torchbearers who would be carrying the Olympic torch across the UK.

The job of a journalist is to find engaging stories which matter. And these pages - thousands of human stories of achievement and inspiration - looked like something I could work with. But the role of a journalist is also to be skeptical, and to hold power to account. And when analysed in aggregate, these thousands of stories also provided an opportunity to ask an important question: were the organisers of the torch relay meeting the promises they had made?

Scraping those thousands of webpages, and putting the results into a structured dataset, was the first step in being able to answer those questions. The stories that resulted from that day in Manchester (documented in the short ebook [*8000 Holes: How the 2012 Olympic Torch Relay Lost its Way*](http://leanpub.com/8000holes)) present just a few examples of the hundreds of ways that scraping techniques can be used to shed light on issues and engage audiences in ways that might otherwise not have been possible.

From Adrian Holovaty's seminal crime map 'mashup' [ChicagoCrime.org](http://www.holovaty.com/writing/chicagocrime.org-tribute/) to stories on [the singers with the biggest vocal range](http://www.mirror.co.uk/news/uk-news/singer-best-vocal-range-uk-4323076); from reports on [the impact of gender and ethnicity on RateMyProfessors ratings](https://www.insidehighered.com/news/2016/03/04/study-links-professors-race-and-gender-brilliant-and-genius-ratings-ratemyprofessors) and [the impact of cuts to library funding](http://www.thebookseller.com/news/8k-library-jobs-lost-due-closures-325187) to [the most festive cities on Instagram](http://www.bbc.co.uk/news/uk-england-35112577) and [the most effective way to get a date on a dating website](http://www.bbc.co.uk/news/technology-31361012), scraping can be used for stories in every field, and of every type: whether serious or frivolous, the results of months of work or a few minutes of playing around.

The widespread digitisation of information, and its publication online, has made scraping an increasingly important tool in a modern journalist's skillset. It allows us to get closer to those facts, in ways that previously were simply not possible, by fetching and organising the information in a structured format.

But before I go any further, I should probably explain a little more what 'scraping' *is* exactly...

## Your own robot

Have you ever wanted a robot to perform the repetitive, time-consuming tasks you hate doing? Tasks that stop you from pursuing key questions in your field, such as where the money goes, or whose names crop up most often in a regulator's reports? Perhaps you'd like a robot to save you the time-consuming process of combining hundreds of spreadsheets into one easy-to-interrogate one? Or to comb through thousands of documents looking for any mention of a particular issue, person or company?

Perhaps your robot would just grab a table or two from the web and put it in a spreadsheet to save you a few clicks in your day-to-day work, or do things more quickly than your competition so you get to a story first.

Scraping - getting a computer to capture information from online sources - is that robot. You tell the scraper what to do, and how to do it, then sit back and get on with the things that cannot be automated, like speaking to sources or reading up on how a particular set of data has been gathered, or reports prepared.

It is not exactly *Wall-E*, but it is used much less often than the other three ways to get hold of data (from a source, via access to information laws, or through advanced search techniques). And it is probably the most powerful way for journalists to get hold of information.

Scraping is *faster than FOI*, provides *more granular results* than most advanced searches - and allows you to grab data that organisations would sometimes *rather you didn't have*.

Oh yes, I like that last one too.

It also allows you to collate and analyse information that no one may have collected before: notices, mentions, documents, relationships, decisions - in fact, anything that's been digitised. That information might be stored in all sorts of ways: tables buried in PDFs and webpages, information hidden behind search forms, or scattered across hundreds of pages or spreadsheets with no single link to them all. What is notable about scraping is that it is not just about grabbing data from online sources - it's also about putting it into some sort of structure. Because what we really want to do is ask it questions.

And if you're curious, and deadlines and topicality are important to you, then scraping is a wonderful skill to have.

## A book about not reading books

I was moved to write this book when I noticed many journalists were trying to learn scraping and programming but struggling to get a foothold - or losing momentum once they did.

As an educator it struck me that many were losing motivation either because they weren't getting results quickly enough, or because there was too much to learn all at once.

As people who typically have a humanities-based educational background - and I include myself here - journalists approach learning in a particular way. If you want to learn a subject such as history or English, you read a book. But programming cannot be learned from books alone.

People learning programming read books, yes, but that's not all: they experiment and solve problems. In fact, the books are often there as a *resource* for when they are solving problems, rather than the focus of learning.

The best advice for anyone seeking to learn scraping or data journalism, then, is this: find a problem to solve first.

This book is designed to help you tackle the obstacles you will find in typical scraping problems. It is structured as a series of tasks, each of which makes up a chapter, and each of which produces tangible results.

Starting from very simple scraping techniques which are no more complicated than a spreadsheet formula, and taking in tools from Google Drive to OutWit Hub along the way, the book introduces you to different programming principles as and when they are needed. You'll be scraping within 5 minutes of reading this - but it's what you learn from that, and how you build on it, which is the really important thing.

Unlike general books about programming languages, everything you learn here will have a direct application for journalism, and each principle of programming will be related to their application in scraping for newsgathering.

And unlike standalone guides and blog posts that cover particular tools or techniques, this book aims to give you skills that you can apply in new situations and with new tools.

Because programming is not about simply knowing a language - it is about a way of looking at problems, diagnosing them, and solving them. If you were used to getting things right first time in school and college, get unused to it: half of the skill with scraping - and half the fun - is working out why things went wrong. And things always go wrong.

There is a saying I particularly like on this subject: *Pulvis et umbra sumus*:

>"*To know what to ask is already to know half.*"

This book aims to teach you not just the principles of programming but the practices; the questions to ask when tackling scraping problems; and the places to ask them.

## I'm not a programmer

Although this book covers some principles of programming, I'm not a programmer: I'm a journalist and educator who uses programming to get hold of information.

That means I sometimes do or explain things in a way that some programmers might find ungainly.

So, two things you need to know: if you're a programmer and something in this book bothers you - let me know. I have done my best to check that my explanations make sense to programmers as well as journalists - but the book is not aimed at programmers.

That means that, although it is important to get the terminology correct, it is more important for a journalist that something works and makes sense. And so I have aimed to simplify things wherever possible rather than bog down things with details or debates which add nothing for the beginner.

For example, scraping itself is known by various different terms, which are often a source of conflict - is it "screen-scraping"? Or "data mining"? Whatever you call it, for the purposes of this book scraping is used generically to refer to the process of grabbing information from a file (a webpage or document) or a series of files.

Because the nature of those files can vary so widely, scraping itself varies enormously as well. The technical challenges of grabbing numbers buried in hundreds of PDFs that are only accessible through a search interface are very different from the challenges involved in grabbing data from a series of tables all linked from the same page.

We'll tackle a number of different challenges as we go through the book - starting with something very simple: scraping a table from a webpage.

As we do that we'll be introduced to the two pieces of jargon I want you to understand first: functions, and parameters. You will be using both from the start, and understand how they form the basis of most scraping.

## PS: This isn't a book

Oh, before that? One more thing: this book is a work in progress. You can download new chapters as they are published, but more importantly, you can influence what gets written and how. If you find any mistakes, or things you want added or explained further, let me know through any of the following ways:

+ On the Facebook page for this book at [Facebook.com/ScrapingForJournalists](http://www.facebook.com/ScrapingForJournalists)
+ On Twitter [@paulbradshaw](http://twitter.com/paulbradshaw)

Now, let's begin.
