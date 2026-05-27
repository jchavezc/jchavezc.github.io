---
layout: page
title: Modeling the Limit Order Book 
description: from a Microscopic Scale
img: assets/img/LOB_cover.jpg
importance: 1
category: work
related_publications: true
---

To understand this project, we first need to talk about what is a Limit Order
Book (LOB) and how it relates to the price formation process.

The evolution of trading markets has progressed considerably in the last few
decades. One of the main drivers of such evolution has been the creation and
usage of fast-paced technological developments. In the past, liquidity was
provided by the so-called market makers, which collected buy and sell orders
from all market participants to set bid and ask quotes. While this traditional
method was generally accepted, mainly, because of the lack of alternatives, it
was also criticized due to the bias and questionable conflict of interest from
the market maker. Nowadays, most exchanges use completely automated platforms
called Electronic Communication Networks (ECN). These ECN enables a continuous
double auction trading mechanism, which eliminates the need of a market maker
or an intermediary that matches the opposite parties in a trade. The auction
that the ECN manages is called "continuous double" since traders can submit
orders in form of bids (i.e., buy orders) as well as asks (i.e., sell orders)
at any point in time. ECNs increase significantly the speed of trading, taking
only a few milliseconds from sending an order to its execution.

A bid limit order (resp. ask limit order) specifies the quantity and the price
at which a trader wants to buy (resp. sell) certain asset. The limit order
book consists of all the collection of limit orders from every trader.
Outstanding limit orders are stored in different queues inside the order book.
These queues are ordered by the price and type (bid or ask). The difference in
price between the lowest ask price and the highest bid price is called the
spread.

The counterpart of limit orders are market orders, which allow traders to buy
and sell at the best available price. While limit orders will not trigger an
immediate transaction, market orders are immediately executed. In this sense,
limit orders accumulate, create, and extend the size of queues at both sides
of the LOB, while market orders remove limit orders from the best available
price. Sometimes informed traders are associated with traders that place
market orders, while uninformed traders are associated to the ones that place
limit orders, but this goes against the fact that many of the most successful
hedge funds make extensive use of limit orders.

In addition to limit orders and market orders, cancellation of limit orders is
another common operation. The basic idea of a cancellation is that a trader is
no longer willing to buy or sell at the specified price. Cancellations account
for a large fraction of the operations on an order book, partly due to the
introduction and evolution of high frequency trading, in
which the inter-arrival times of limit orders and cancellations, occur at a
millisecond time scale.


A pictorial representation of the LOB can be seen in the following figure.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/LOBExample.jpg" title="Representation of a Limit Order Book" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The image represents the LOB as a queueing system.
</div>




The resulting published work from this project on my side can be found in {% cite chavez2019level %},
{% cite chavez3 %}, {% cite chavez2024CompEc %} and {% cite Chavez1 %}. 





Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
