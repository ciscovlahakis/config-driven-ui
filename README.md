This is the first part of the 2 part blog, where I share my experience in putting together a configuration driven user interface.

The solution consisted of the actual UI that is generated by configuration and admin app where a user can drag and drop to build the configuration. 
This blog specifically talks about how we handled the UI based on a JSON configuration.


## The Problem

Our customer wanted to build an enterprise dashboard that would help them to see display different dimensions of data in different pages. 
Each page can follow a different layout consisting of Titles and it's corresponding  Visualizations or summary.
 

One of their most important requirement was to have minimal or no dependency on developers for putting together these pages. 
They had a few super users, who were good with writing queries and wanted to build a system that would help them to build a dashboard on their own. 

# 10,000ft Solution
A part of our solution looked something like below. 

![Solution Blocks](./solution-blocks.png)

The DnD Config Generator provides the user a UI where they can assemble the UI components together. 
With the generated JSON configuration, a service call is made, which persists the same into a database. 

When the executive dashboard needs to display the UI, it makes a restful call to the backend, which delivers the corresponding JSON from the database. 


## The Config Driven UI

We wanted to solve the configuration driven UI first, to understand what kind of configurations were required and take that as a cue while putting together the config generator. 
So we started to break down our problem and came up with 2 major components. 

* Building the Layout
* Filling the gaps in the layout with actual values such as titles, visualizations and summary. We call this as an __Element__. 


### Layout
    
The layout consisted of a bunch of elements that were stacked vertically, or horizontally. 
So we needed to have containers that would let to stack the elements either vertically or horizontally. 
There are also cases where we wanted to stack the Vertical / Horizontal containers inside each other or within themselves.

![Layout example](./layout.png)

In the above example we have a vertical container that has elements E1 and E4 stacked vertically, along with a horizontal container H1.
H1 in-turn stacks in the elements E2 and E3 horizontally. 
  
To achieve this we needed a recursive JSON configuration.
  
