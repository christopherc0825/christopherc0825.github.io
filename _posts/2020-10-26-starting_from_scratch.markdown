---
layout: post
title:      "Starting from scratch"
date:       2020-10-26 21:03:40 +0000
permalink:  starting_from_scratch
---


This post is following my first dive into Javascript. Everyother programming language I've encountered has had best practices and guidelines to follow when programming and as a creature of habit this is something I relied on heavily. However, enter stage right is Javascript, or the wild wild west of programming where there's always another way to complete something you're working on.

Lets begin with the biggest thing JS has to offer, functions. You have a variable? That's a function. You have an argument to a function? That's also a function. This concept took awhile to click but once it does it allows a lot of abstraction as JS treats functions as first class data just like the primitive datatypes.

While JS seems complicated, its simplicity is what causes it. JS has a very small number of primitive types and nothing is type casted meaning you can do 1+1 and get 2 or 1+'two' and get '1two'. Coming from Java, Ruby, and .NET this is a big change and takes a lot to get used to.

So... onto my project. I started with a blank HTML page as my goal was to build everything with JS. Therefore I started with building out a class that built my HTML elements for me.

```
class htmlFactory {
    static build(tag, klass, id, content = null){
        let element = document.createElement(tag)
        element.setAttribute('class', klass)
        element.setAttribute('id', id)
        if(content){
            element.innerText = content
        }
        return element
    }
}
```

After this was said and done I built my form with a function and used a fetch method to retreive all the posts in my data base and went from there.

Once I got an object containing all my JSON from the DB I can use my HTML factory to build out the elements and append them to my page

```
const createPostCards = function(posts){
    let postsArr = posts.data.reverse()
    for(const post of postsArr){
        let div = htmlFactory.build('div', 'card', `post-id-${post.id}`)
        let title = htmlFactory.build('h3', 'card-title', `card-title-${post.id}`, post.attributes.title)
        let content = htmlFactory.build('p', 'card-content', `card-content-${post.id}`, post.attributes.content)
        let comments = htmlFactory.build('ul', 'comment-list', `comment-list-${post.id}`)

        main.appendChild(div)
        div.appendChild(title)
        div.appendChild(content)
        div.appendChild(comments)

        for(const comment of post.attributes.comments){
            let li = htmlFactory.build('li', 'comment', `comment-id-${comment.id}`)
            comments.appendChild(li)
            li.innerText = comment.content
        }

        div.addEventListener('click', () => {
            fetchPost(post)
        })
    }
}
```

Then after following the same logic for the comments the web app works and we survived high noon in vanilla Javascript.

