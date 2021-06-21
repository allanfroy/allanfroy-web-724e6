+++
date = 2021-05-23T23:49:00Z
excerpt = ""
image = "/images/volodymyr-hryshchenko-v5vqwc9gyeu-unsplash.jpg"
image_alt = ""
layout = "post"
subtitle = ""
thumb_image = "/images/volodymyr-hryshchenko-v5vqwc9gyeu-unsplash.jpg"
thumb_image_alt = ""
title = "3 secrets to event-driven thinking - Pt 2"
[seo]
description = ""
extra = []
robots = []
title = ""
type = "stackbit_page_meta"

+++
But my consumers need this data.....

Why are very clever software professionals seemingly struggling with the concepts of EDA? Those with a good grounding in domain-driven design seem to find the leap easier. Those coming from a starting point in REST APIs, large enterprise database solutions, or even 12-factor applications may find event thinking at odds with what they already know.

I'm posting short dialogues that highlight the 3 most common challenges I see in understanding event-driven thinking. Part 2 looks at letting consumers dictate the contents of an event.

**_No. 2 - Consumer driven events_**

Tell me a bit about how you determined what information should be in the event payload you're publishing.

Ok, so we looked at the existing 3 downstream systems and pieced together a new data model from the data each system requires. Then we looked at the analytics needs and added some extra attributes so we can get great insights. Simple really!

Great. How well does that information match the internal state of your microservice?

Well it does mostly, we think. There might have been a few things we had to tweak. Oh, and we had to pull in some data from this other service to make sure everything was populated, but other than that it's a pretty good match.

What happens if another consumer comes along and needs to work with your events?

Oh, we're not expecting that anytime soon so we're not planning for it. I guess we'll just have to update our internal state to include any new requirements.

I see. So you're compromising the integrity of your microservice because of the few known consumers each with different requirements. And you have no way of dealing with new consumers that might come along with further requirements. Sounds fragile to me.

> Letting consumers dictate the event payload leads to fragile systems

How about you take control of the data model within your service and publish an accurate representation of that in the event instead. Start by considering that you have no consumers at all or that you have 1,000 - either way, as you publish the event, you shouldn't care if anyone even notices it.

Sure some consumers might need to enrich your data with other data from other services. Great! Let _them_ do that in an event-driven architecture - the consumer has the power to do what it wants with your events without compromising the processing of any other consumer, or indeed of the producer.

Use an inner-source model to let consumers suggest changes to the event payload. Ultimately the decision on whether that change makes sense lies with the producer, since they are the subject matter experts in their domain.

To build an anti-fragile system events must be driven by the producers. Yes, you can use knowledge of consumers to inform the event design but don't compromise the integrity of the service in doing so.