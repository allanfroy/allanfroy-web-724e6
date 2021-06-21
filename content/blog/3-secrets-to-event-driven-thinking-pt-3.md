+++
date = 2021-06-21T02:27:00Z
excerpt = "I'm posting short dialogues that highlight the 3 most common challenges I see in understanding event-driven thinking. Part 3 examines the nuanced differences between orchestration and choreography when working with events."
image = "/images/volodymyr-hryshchenko-v5vqwc9gyeu-unsplash.jpg"
image_alt = ""
layout = "post"
subtitle = ""
thumb_image = "/images/volodymyr-hryshchenko-v5vqwc9gyeu-unsplash.jpg"
thumb_image_alt = ""
title = "3 secrets to event-driven thinking - Pt 3"
[seo]
description = ""
extra = []
robots = []
title = ""
type = "stackbit_page_meta"

+++
I can orchestrate with events just like I can with APIs.....

Why are very clever software professionals seemingly struggling with the concepts of EDA? Those with a good grounding in domain-driven design seem to find the leap easier. Those coming from a starting point in REST APIs, large enterprise database solutions, or even 12-factor applications may find event thinking at odds with what they already know.

I'm posting short dialogues that highlight the 3 most common challenges I see in understanding event-driven thinking. Part 3 examines the nuanced differences between orchestration and choreography when working with events.

**_No. 3 - Event orchestration vs collaboration_**

I need to make sure the user goes through all of these steps in the right order. There's a set workflow.

Great! How are you going to co-ordinate the workflow for each user?

I was thinking we would need a central service that makes API calls and/or uses events to co-ordinate across the required services.

Right, so you've got the whole workflow documented in one place, that seems sensible. How many teams are involved in the process?

Well, we've got the team handling the different orders, then there's a separate team that handles the payments and finally there's the shipping team.

Ah, so you need to co-ordinate across these different teams too. This is easier if all of the steps fall within the same domain and particularly where all of the services are owned by the same team. It's more difficult when one or more of the steps sit across multiple domains and owning teams. You shouldn't be making API calls across domain boundaries so I would recommend focusing on the events.

Ok, that makes sense. So we'll just emit events from the workflow service to tell each service what they need to do.

That would indeed be an orchestrated way to do it, but those are commands not events. Because the process can't be owned by any one team think about devolving the workflow into the individual services instead. The order service can emit events that trigger the payments service and the shipment service would only be triggered once the payment service has updated the order.

![No alt text provided for this image](https://media-exp3.licdn.com/dms/image/C5612AQGk-hlnP46jeQ/article-inline_image-shrink_1000_1488/0/1624242191778?e=1629936000&v=beta&t=M7iDFbWpkIzFervkJP7UmPwWFC31FGrFjg8-xn12dFY)

_(Above image sourced from Ben Stopford's_ [**_blog series_**](https://www.confluent.io/blog/build-services-backbone-events/) _and_ [**_book on Designing Event-Driven Systems_**](https://www.confluent.io/designing-event-driven-systems)_)_

But doesn't that make it more difficult to keep track of the whole workflow?

It's a different way of looking at it, mainly because of the different teams involved. Instead of orchestrating you are choreographing the different services. Each service is responsible for it's own subset of the workflow and when you look across them all you can see the full business workflow. From a service perspective none of the services knows anything about the others and equally there is no one service that knows about the whole process. To combat this the business process should be fully documented as an aid to all of the software teams involved in the implementation.

Oh I get it. It allows each of the teams to continue to develop their own services independently as long as they commit to maintaining their part of the bigger workflow.

Exactly! But remember both choreography and orchestration are valid patterns that should be applied to the right use cases. As a rough rule of thumb you can orchestrate within the same bounded domain and you should choreograph across multiple bounded domains.

### Summing Up

This was a three part series exploring some of the common challenges I see to people adopting an event-driven mindset.

* Part 1 - Commands dressed as events - be mindful of crafting events that are really just commands in disguise
* Part 2 - Consumer-driven events - focus on events that accurately represent the state of the producer, not what a myriad of current or future consumers might need to see in that event
* Part 3 - Orchestration vs collaboration - orchestration services are a goto solution from the API way of thinking, remember that events are a different form of communication and you may not need a central service to describe your business workflow