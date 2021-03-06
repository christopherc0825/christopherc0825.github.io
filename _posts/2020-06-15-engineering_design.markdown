---
layout: post
title:      "Engineering Design"
date:       2020-06-15 23:56:26 +0000
permalink:  engineering_design
---


If you are reading this I can only assume you are and engineer and design is the bane of your existence. Welcome to my Sinatra web app where design was an implied requirement.

Luckily there are many frameworks such as bootstrap that can help you through designing the looks of your application. However, to try and get a better grasp of *being creative* I decided to skip the framework and use vanilla css to get my app how I wanted.

To build my app I used a gem made by a Flatiron graduate called Corneal which gave me my file system and a basic barebones app to build off of. When I started to style my app I noticed there was a file in my stylesheets already. I figured that this was it I don't need anymore design to go into this. However, I was wrong so I had to dip my feet into CSS.

The gem gave me 2 breakpoints one for the screen and one if the screen is under 600px. This was using `@media screen` do determine the size of the screen the app was using from there it gave me some reset styles and the rest was up to me.

Fortunately, the content of my app was styled and the background matched the icon I was using. This means all I have to do is the navbar which still turned out to be quite the hassle getting it to look nice.

```
<nav>
    <div class="navbar">
      <img src="/images/favicon.ico" alt="Teddy Bear Repair Logo">
        <% if logged_in? %>
          <a href="/user/dashboard">Dashboard</a>
          <a href="/user/dashboard/edit">Edit User</a>
          <a href="/logout">Logout</a>
        <% else %>
          <a href="/login">Login</a>
          <a href="/user/new">Register</a>
        <% end %>
      </div>
    </nav>
```

This is what I had to work with. A simple div containing links and the logo. Easy enough I figured I could do it all in the nav selector. well theres a little more that would go into it.

To get a nice background for the bar I added it to the nav selector. I also got rid of padding, margin, and overflow.

```
nav {
    background: #eee;
    margin: 0;
    padding: 0;
    overflow: none;
  }
	```
	
Then moving on to make sure everything was nice and centered I added a flex display to the div inside
	
```
nav div.navbar {
    display: flex;
    align-items: center;
  }
```

Now at this point I have a bar with a white background with some links going across it. At this point I need to style the links so lets move on to the selector nav a

```
nav a {
    display: block;
    color: #333;
    padding: 16px;
    text-decoration: none;
  }
```

Here I set the display to block which makes the whole area clickable and the text color to black with a padding of 16px on each block. I also removed any text decoration.

At this point everything is looking nice but it could be a little better so lets invert the link when hovered over. Luckily, CSS makes this very simple with its relative selectors making something like this possible 

```
nav a:hover {
    background-color: #333;
    color: #eee;
}
```

So that was nice and painless and makes me ready to move forward with a little more *creative* elements in my future projects.

