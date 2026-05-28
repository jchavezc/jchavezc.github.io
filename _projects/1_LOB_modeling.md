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

# An introduction to Limit Order Books (LOB)

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
   Graphical representation of a Limit Order Book. The Bid Limit orders (to the left) are displayed in blue, while the Ask limit orders (to the right) are displayed in red.
</div>


To better understand the dynamic behaviour of the LOB the following example, 
taken from {% cite Abergel2011 %}, is presented.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/LOBdevelop.png" title="Operations in a Limit Order Book" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   A possible evolution of the LOB. First, a large Ask Market order arrives, taking out liquidity and causing the spread to widen. Then, a small Ask Limit Order arrives, followed  by a Cancellation on the Bid side. Finally, Ask and Bid Limit orders are posted within the spread, causing this to reduce in length.
</div>

As illustrated from the figure, the different types of operations in a LOB may
or may not affect the prices. Understanding how these operations affect these
best prices is crucial in developing a parsimonious model for the price
dynamics. Consider, for example, a buy (resp., sell) limit order arriving at a
certain time $t$ with price $p_t$. Let $a_t$ and $b_t$ denote the current price
of the best ask and bid at time $t$. Moreover, let also $s_t = a_t - b_t$ denote
the bid-ask spread at time $t$ and assume, for illustration purposes, that
$s_t > 1$. If the arriving order has price $p_t < b_t$ (resp., $p_t>a_t$) then
it will increase the amount of outstanding limit orders at
price $p_t$. However, if $b_t < p_t < a_t$, that order will become the
best bid (respectively, best ask), hence, increasing (resp. decreasing) the
mid-price. On the other hand, if the order is a market order to sell (resp.,
buy), this will decrease the amount of orders at the best bid (resp., ask). In
this case, the price should match $b_t$ (or $a_t$, resp.) since traders will
not sell something cheaper if they can sell it more expensive (resp. pay more
for a stock that can get for a cheaper price). Moreover, if such order is large
enough it may deplete several bid levels of the order book decreasing the best
bid price (resp. depleting several ask levels of the orderbook increasing the
best ask price).

An important feature of a LOB is that traders can choose between submitting
limit and market orders. The biggest advantage of limit orders is the
possibility of matching better prices than the ones they can obtain with market
orders, but as drawback, there is a risk of never being executed. Conversely,
market orders never match at prices better than the best bid or the best ask,
but the execution is certain and immediate. Usually, the bid-ask spread can be
considered as a measure of how expensive is the certainty and immediacy of
buying or selling the underlying asset.

# A plausible model of the LOB

From a modeling perspective, sometimes it is important to identify the
different types of traders that are able to participate in the market. LOBs 
allowed traders to immediately obtain
liquidity, but at the same time, they also allow other traders to supply
liquidity to those who require it later. On the exchanges, most traders combine
limit orders and market orders to create a trading strategy according to their
needs and the current state of the order book. However, broadly speaking, traders 
with short-horizon strategies, as arbitrageurs,
technical traders, and indexers, prefer to post market orders, while, traders
with long-horizon strategies, as portfolio managers, place limit orders.

There are many practical advantages in understanding LOB dynamics. Examples of
these are: gaining clearer insight into how best to act in a given market
situation, devising optimal order execution strategies or optimal placement
strategies, minimizing the market impact; designing better electronic trading
algorithms, and assessing market stability.

In terms of modeling, we can follow a classical approach of a toy model as presented in 
{% cite ContLarrard2012 %}. In here, we can do an overarching model as presented below:

- Let ${}^{a/b}L_t^{(n)}$ be the process that define the arrival or Limit Orders at the $n-$th level of the ask/bid side of the orderbook.
- Similarly, ${}^{a/b}M_t^{(n)}$ will denote the processes determining the arrival of Market Orders at the $n-$th level of the ask/bid side of the orderbook.
- Also, let ${}^{a/b}C_t^{(n)}$ be the process driving the cancellations at the the $n-$th level of the ask/bid side of the orderbook.

In terms of the volumes, we can denote by

- ${}^{a/b}V_t^{(L\;;\;n)},{}^{a/b}V_t^{(M\;;\;n)}$ and ${}^{a/b}V_t^{(C\;;\;n)}$  the volume of the corresponding limit order, market order or cancellation arriving at the ask or bid side at level $n$.

Another imnportant quantity that we need to keep track of is the current volume at the order book. With this is mind,

- Let ${}^{a/b}Q_t^{(n)}$ be the amount of outstanding limit orders at time $t$ at level $n$ on the ask/bid side. 

Finally, we need to account for the time the price changes occur and understand their statistical properties. Indeed,

Let $\sigma_1^{(a/b)}$ be the first time that a price change occurs from the ask or bid side. That is,

- let $ \sigma_1^{(a/b)} = \inf\left\\{ t \geq 0 \mid {}^{a/b}Q_0^{(1)} + {}^{a/b}L_t^{(1)} - {}^{a/b}M_t^{(1)} - {}^{a/b}C_t^{(1)} = 0 \right\\}$.

Notice that $\sigma_1^{(a/b)}$ is indeed the firt time a price change from the ask/bid occurs
as it becomes the first moment that Market Orders and Cancellations from the ask/bid at level 1 
deplete the available number of original Limit Orders at level 1 plus the further Limit Orders 
at level 1 that have arrived at the corresponding side of the book. Then, naturally, the
first time a price change occurs is 

- $ \tau_1 = \min\left\\{ \sigma^{(a)}_1, \sigma^{(b)}_1 \right\\}$


In this fashion, we can continue quantifying when price changes occur on the LOB. Define recursively

- $\sigma_{n+1}^{(a/b)} = \inf\left\\{ t \geq \sigma_n^{(a/b)} \mid {}^{a/b}Q_{\sigma_n^{(a/b)} }^{(1)} + {}^{a/b}L_t^{(1)} - {}^{a/b}M_t^{(1)} - {}^{a/b}C_t^{(1)} = 0 \right\\}$

and

- $\tau_{n+1}=\min\left\\{\sigma^{(a)}_n,\sigma^{(b)}_n \right\\}$.

So, if we denote by $\\{X_n\\}_{ n\geq 1 }$ the amount by which the price changed right after the $n-$th price change $\tau_n$ and by $\\{S_t\\}_{t\geq0}$ the price process, then it is clear that

- $S_t=S_0+\sum\limits_{k=0}^{N_t} X_k$,

where $N_t=\max\\{n \mid \tau_1+\tau_2+\ldots+ \tau_n\leq t\\}$. Indeed, $N_t$ just counts how many price changes have occurred up to time $t$ and the price at time $t$ is the starting proce $S_0$ plus all the changes that have occurred so far.

Notice that in essence, this is a very open model and our specifications on the dynamics of the Volumes, the Arrival processes, the distribution and statistical properties of Price Changes and their dependencies among themselves can be broadly specified, and what we would like is to understand how these inter-dependencies play a role in generating the different price process models used on a diffusion-limit scale.

# What are some relevant questions regarding this model?




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
