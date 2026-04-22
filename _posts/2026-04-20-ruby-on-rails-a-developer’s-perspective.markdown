---
title: Ruby on Rails - A Developer’s Perspective
date: 2026-04-20 09:00:00 Z
categories:
- Technology
tags:
- Technology
- Software Development
- Ruby on Rails
- Web Development
- Rapid Development
summary: I recently picked up Ruby on Rails for a client project, and it turned out to be a more enjoyable experience than I had expected.
author: mthomas
image: 
---

After more than five years building production systems with Java and working across a range of backend and cloud technologies, I’ve developed a healthy habit of approaching new frameworks with both curiosity and scepticism. That mindset guided me when I recently upskilled in Ruby on Rails for a potential client project — and the experience turned out to be more interesting than I’d anticipated.

## What Ruby on Rails Actually Is

Ruby on Rails (commonly just called Rails) is an open-source, server-side web application framework written in Ruby. It follows the Model–View–Controller (MVC) architectural pattern and is heavily opinionated in how applications should be structured. Its core design principles are:

- **Convention over Configuration**: many decisions are made for you by default

- **Don’t Repeat Yourself (DRY)**: duplicate logic is actively discouraged

- **Full‑stack by default**: database layer, routing, controllers, views, background jobs, and testing tools are all integrated

Rails was first released in 2004 and, despite regular claims of decline, remains actively maintained and widely used. As of March 2026, Rails 8 is the current major version, with continued investment in performance, security, and modern development practices.
What distinguishes Rails from many frameworks is not novelty, but maturity. Its patterns have influenced frameworks across ecosystems, including Django (Python) and Laravel (PHP).

### Where Ruby on Rails Is Used Today

Rails is not a niche framework confined to hobby projects. It is used in production by companies operating at global scale, particularly where rapid feature development and stable long-term maintenance matter.
Notable organisations using Rails include: _GitHub,Shopify,Airbnb,Basecamp,Twitch_

In today’s market, Rails is most commonly used for:

SaaS platforms, especially MVPs that need to reach market quickly
Content-heavy applications with complex business logic
API-driven systems, where Rails acts as a robust backend for mobile or JS-heavy frontends
Internal platforms and tooling, where maintainability and developer productivity outweigh raw throughput

Rails has also adapted well to modern infrastructure expectations—containerisation, background job processing, caching, and cloud-native deployments are all first-class concerns in current versions. [en.wikipedia.org]

## My Journey

Experimenting with Ruby on Rails quickly became something of a love–hate relationship.

At first, I was impressed but deeply sceptical. The generators felt almost too good to be true — models, controllers, and test files appearing instantly was undeniably satisfying. At the same time, it created a nagging sense that a lot was happening “behind the curtain,” with important details carefully hidden away by convention.
That initial discomfort didn’t take long to turn into frustration once the magic broke. When something behaved unexpectedly, the error messages didn’t always point back to code I had written. Instead, I found myself reverse‑engineering framework behaviour, trying to understand decisions Rails had already made on my behalf rather than reasoning directly about my own logic.
Over time, though, that frustration softened into acceptance. Rails isn’t inherently problematic; it simply asks for a different kind of trust. You’re encouraged to lean into its conventions, slow down, and learn its way of doing things — even when that way feels opaque at first.

That tension is what makes Rails such a paradox, and oddly, a delightful one.

It’s incredibly productive. I was able to get a working solution up and running in a fraction of the time it would have taken to hand‑code the same functionality elsewhere. 
Scaffolding and boilerplate were handled effortlessly, leaving me free to focus on the shape of the problem rather than the mechanics of wiring things together.
At the same time, it hides a significant amount of complexity. You can make rapid progress without fully understanding the underlying architecture or design patterns at play, which is both empowering and dangerous. That hidden depth only really reveals itself when you need to debug something subtle or push the framework beyond its happy path.
And while Rails is undeniably friendly to beginners, it can feel surprisingly opinionated to experienced developers. Getting started is easy, but stepping outside the rails — quite literally — can feel like pushing against the framework rather than collaborating with it. That tension is where most of my friction lived.

### Key Insights

#### Generators
One of the most immediately striking aspects of Rails is how much productivity it unlocks through conventions and tooling. The framework’s generators, backed by Active Record, remove a significant amount of boilerplate that developers in other ecosystems are often accustomed to managing explicitly.
For example, a single command:

`generate model Product name:string`

creates a model, a corresponding test file, a database migration, schema updates, and the necessary directory if they do not already exist. 
It also lays the groundwork for standard CRUD operations. This level of automation can feel surprising at first, particularly coming from environments where each of these steps must be wired together manually.
Active Record, Rails’ ORM, plays a role similar to Hibernate or JPA in the Java ecosystem, but with far less visible configuration. 

#### Associations and Data Modelling
Relational modelling can be expressed in a small amount of highly readable code:

``` 
class Product < ApplicationRecord
  belongs_to :user
  has_many :line_items
  has_one :profile
  has_many :orders, through: :line_items
end
```
Despite its simplicity, this definition establishes associations, infers foreign keys, generates migrations, and enables cascading deletes. SQL is abstracted away entirely unless you explicitly choose to drop down to it. The emphasis on convention means configuration becomes largely implicit, shifting focus away from setup and towards domain modelling.
Associations are where Rails feels particularly expressive. Relationships such as belongs_to, has_one, has_many, and has_many :through read almost declaratively.

Rails transparently manages the primary and foreign key relationships behind the scenes, while the database ensures data integrity. Features such as 
`dependent: :destroy` stood out to me, as they allow cascading behaviour to be expressed clearly in code without introducing additional complexity at the database layer.

#### Rails Console and Debugging
Rails also provides a powerful interactive environment through the rails console, which loads the full application context and database connection. It can be used to query, inspect, and manipulate application state in real time:

```
Product.firstProduct.create(name: "Cupcake", stock: 12)
Product.last.destroy
```

This eliminates the need for ad‑hoc scripts or temporary endpoints during development and debugging. The feedback loop is fast, direct, and tightly integrated with the application itself.

The documentation often emphasises logging and console‑based inspection for debugging, which can feel limiting if you are used to IDE‑driven debugging workflows. However, with the addition of VS Code Ruby and Rails debugging extensions, the experience becomes much more aligned with what developers expect from mature IDE tooling. Breakpoints, variable inspection, step‑through debugging, and thread visibility are all available, with the added benefit of the Rails console running alongside the debugger.

### Comparing SpringBoot and Rails

When working with Ruby on Rails felt both familiar and disorienting in equal measure. The high‑level architectural concepts — MVC, layered responsibilities, and REST‑centric design — are recognisable, but the way Rails guides you towards those outcomes is markedly different.
The most immediate difference was how much Rails removes up‑front decision‑making. As a Spring developer, I’m used to explicitly defining configuration, wiring dependencies, and making architectural intent visible through annotations and structure. Rails, by contrast, leans heavily into convention over configuration. At first, this felt uncomfortable — almost like important details were being hidden. Over time, though, it became clear that Rails isn’t removing complexity so much as delaying it until it’s actually needed.

ActiveRecord was another notable shift. Compared to Hibernate/JPA, it’s far more opinionated and tightly integrated into the framework. It’s designed to be simple and intuitive for common use cases, but it can feel restrictive when you need to do something unconventional. In contrast, Hibernate/JPA offers more flexibility at the cost of simplicity.
Rails’ ORM significantly reduced boilerplate and allowed features to be delivered quickly with minimal ceremony. The trade‑off is that you need to be disciplined in understanding what the framework is doing on your behalf — especially as data access patterns become more complex.

The framework, tooling, and ecosystem are optimised to get something working end‑to‑end quickly. Compared to Spring Boot, where robustness and explicit configuration reinforce enterprise safety, Rails prioritises momentum. For early‑stage development or well‑bounded domains, this feels like a genuine advantage rather than a shortcut.

| Aspect               | Ruby on Rails                 | Spring                                      |
|----------------------|-------------------------------|---------------------------------------------|
| ORM                  | ActiveRecord                  | Hibernate/JPA                               |
| Philosophy           | Convention over configuration | Heavy configuration, annotations everywhere |
| Developer experience | Fast prototyping              | Enterprise robustness                       |
| Ideal for            | Rapid CRUD apps               | Complex enterprise architectures            |

## Final Thoughts

In the end, my time with Ruby on Rails was brief but instructive. Just as I was getting truly comfortable, the client project I’d been preparing for failed to materialise, and my short Rails experiment came to an abrupt end. I found myself back in familiar Java territory, my detour complete.
Whether I’ll return to Ruby on Rails one day, or whether it remains the framework that got away, I’ll leave to fate. But one thing I’ll leave you with is this:
Rails may not always be love at first sight, but it’s undeniably efficient. It feels like the older, wiser framework in the room — not flashy, not loud, probably not lining up to give a TED talk to stay relevant — but still deeply competent. Quietly generating files, enforcing conventions, and occasionally making even the sceptics pause and think:
“Okay… that was actually pretty cool.”