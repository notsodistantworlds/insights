# Be my DTO! Be my Entity!

...be both if you dare!

## DTO and Entity are not mutually-exclusive concepts...

...and arguing that they are is a waste of time and resources.

At some point i ended up arguing with someone that a service should return entities,
not DTOs. Since DTOs are controller-layer things and, well, why would the service layer
need to know about them? 

The counter-argument i faced against was very similar: Entities are service-layer objects
and should not be exposed to controllers. Therefore, services may internally operate on
entities but must return DTOs to the calling controller.

I believe i won that debate, at least based on the fact that most of the team agreed with
my point of view. And ultimately, everyone agreed to at least address the source of
this discussion - the fact that our services returned a JsonObject(**never** do that!)

However, i have since reconsidered my way of thinking. The question itself is loaded and
wrong. Acting as if DTOs and Entities are *always* different things is, in my opinion, wrong.
They can be - but they also can overlap, and when they do, that is just fine.

## Persist the entity, respond with DTO

So the way i think about it now is:

Entities are, well, entities. They are clearly defined objects in your solution's model,
and they represent some (usually-real-world) piece of your problem that you're trying to solve.

Entities are usually stored somehow on your server. Usually via an SQL database. But it could
be a file, or a redis with persistence, or even another REST server which offers persistence services.

On the other hand, DTOs are structures sent over to remote services. It's In The Name: "Data Transfer Object".
"Remote services" in that these services aren't directly accessible in your language's runtime, 
and thus you need to use some fancy protocol to get the data across. Usually the protocol in question will be
the good ol' HTTPS.

And the core insight is: Entities can be DTOs, and DTOs can be Entities. Then again, they can also not be.
Don't panic if either is the case. This is object-oriented programming, and declaring unnecessary layer
boundaries for your objects is awkward and wasteful.

That isn't to say that you shouldn't minimize the amount of dependants on your Entity/DTO class if
you get a chance. But it shouldn't be religious, and it shouldn't get in your way of coding the actually
useful stuff.

## Do not fear the POJOs

Better yet: some objects aren't entities, nor are they DTOs. **And that is fine.** This is object-oriented
programming, and objects are your friends(most of the time). If you need a custom object here, then go ahead
and create one. Of course, you shouldn't create a new class every time your hands itch, but when you
feel like it's justified and solves more problems than it causes, you probably should do it.

## Layers are nice. Let's get more of them.

The idea of 3 layers, Controller <-> Service(s) <-> Repository(ies) is certainly nice and helpful,
and it does improve the quality of code, (somewhat) preventing it from degrating into a remarkable 
mess of spaghetti. But focusing too much on these 3 layers is invalid, IMO.

Don't:

 - argue tooth-and-nail about which kinds of objects your Services should return.

Instead, do:

 - track your project's classes' dependency tree
 - analyze it for layers. A layer is a set of classes that mutually care about
 each other.
 - try and minimize the size of each layer if possible. Prefer more layers over larger layers.

This of course only applies to logic-heavy server apps. Applications that are just direct frontends
to a database do not have inter-service dependencies, and arguably could be written without a service
layer anyway.
