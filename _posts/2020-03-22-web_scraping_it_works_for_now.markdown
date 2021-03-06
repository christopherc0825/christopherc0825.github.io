---
layout: post
title:      "Web Scraping:  It works! for now..."
date:       2020-03-22 23:39:16 +0000
permalink:  web_scraping_it_works_for_now
---


Hello, welcome to my second blog post. In this section I will be going over web scraping using nokogiri and hopefully assist people getting over the same hurdles I did when tackling this task.

So lets start off with the biggest thing there will be a lot of back and forth so when you are ready to start coding your scraper be prepared to be debugging for a while.

To get everything started you are going to want to use Nokogiri to get the information from the webpage you want to scrape from using a pretty straight forward command.

```
doc = Nokogiri::HTML(open(url))
```

Now to get this working you will need to require nokogiri and open-uri.

Awesome! now we have a webpage's contents saved into a handy place in memory where we can work from.

From here we will be searching the information we saved to the `doc` variable. This is done by a method in Nokogiri named #css. To use this method we will be inspecting the webpage for tags and classes in the HTML. Luckily for us most developers reuse these classes for items that are similar, this is great that means we can find items that are the same to use for collections.

In my case I was after these

![](https://i.ibb.co/F66nbHn/event.png)

more importantly I was after the links so I could repeat the whole process again for each event page

To do this I had to search the html for useful classes and tags. I realized that the linkes were nested inside an h2 with the class name "tribe-events-list-event-title" hmm easy enough for now the next tag was of course an a tag since i was looking for links. At this point I knew I needed a collection of links that followed this pattern so using the map function seemed like the best bet as it returns an array of the new items working on so my line of code ended up being this

`@links = @doc.css('h2.tribe-events-list-event-title a').map {|link| link['href']}`

So to this point, I scraped the events page for all the links to the events and saved them to an array. Unfortunately, this was only half the work I needed to do to get my program working.

in each of these links was a page containing the name of the event, a date, and a description so I knew I needed to do this for each page so that means I need to use nokogiri to do so on each page. I decided to use an iterator to create an object for each page to make accessing all this information easier (also the project required I do that... but regardless).

Since I did not need to return anything specific and I was simply doing all my work in the block of code the simple each iterator does the job.

Just as a little background I used mass assignment in my Event class so only a hash is passed in to the method instead of a bunch of order specific arguments

```
def initialize(attributes)
        attributes.each {|key, value| self.send(("#{key}="), value)}
        save
end
```

Now to operate on my `@links` array

```
@links.each do |link|
            event_page = Nokogiri::HTML(open(link))
            #:name, :date, :description
            attributes = {}
            attributes[:name] = event_page.css("h1.tribe-events-single-event-title").text
            attributes[:date] = event_page.css("h2 span.tribe-event-date-start").text
            attributes[:description] = event_page.css("div.tribe-events-single-event-description p").first.text
            e = Event.new(attributes)
            @calendar.events = e
end
```

It may seem like a lot is going on here but its really simple once you read through it really the worst part is combing through the web inspector in chrome to find the arguments for nokogiri

Now, what this method does is create a new doc like we did to get the links using Nokogiri. Once its parse it saves the information from the specified areas to a key in a new hash named attributes, then it creates a new Event instance passing in the new hash and then adds it to the calendars events instance variable using an overwritten events= method

```
def events=(event)
        if event.is_a?(Event)
            @events << event
        end
    end
```

This checks to make sure the passed in argument is indeed an instance of Event and adds it to an array for easy management.

So at this point everything is working fine and the program scrapes the information and displays it as it should but then comes the caveat of web scraping.... It's not a static website meaning when they change their website for any reason it has the potential of breaking my program. While it works now... there is no guaranteed longevity to my program. Luckily this is just a portfolio project to demonstrate object relationships and web scraping techniques as the fragility of wweb scraping definitly makes me uncomfortable and would deter me from using it for an end user application.

So in conclusion... It works! for now...

