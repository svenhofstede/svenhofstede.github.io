---
title: Simplicity for the web
date: 2023-04-18
---

Front-end engineering seems terrifying. 

The amount of different frontend frameworks and the speed in which stuff goes out of fashion. The need to write everything in Javascript which is in most cases a completely different language to your backend. The need to even make the distinction between a frontend and backend dev in the first place. Why has it gotten so far?! 

I'm a big fan of keeping the front-end of a web application simple. I'd argue that most web applications is development today don't need to complex frontend app and would do just fine using server-side rendered templates. I've recently used [htmx](https://htmx.org/) together with FastAPI and the experience was great. I definitely had to learn a thing or two along the way but generally it was quite painless. Dynamically returning html snippets from the server just makes **so much sense** in my head. Super complex frontends like large social media websites and big e-commerce websites might be good candidates for an entirely separate Javascript frontends but it's major overkill for small crud applications and needlessly adds complexity. 

I think this is also fed by the existence of code bootcamps who attempt to get a candidate ready for the industry asap. They are taught a Javascript framework to build frontends because there is a lot of open positions in this area. But I don't think these candidates are taught the downsides of this approach and of the existence of server-side rendered alternatives. 

I'm also a big fan of static site generators to serve content. It's lightning fast, costs practically nothing to host and is super safe as no one can comprise the backend.