# All our solids are SOLD

...perhaps try a different shop.

## So much for interface segregation

People like to claim that their code is SOLID, but usually, it is very much not. And while the 
SOLD parts are usually more-or-less there, the one i see most often swept under the rug and
Ignored is the I part(pun not intended, although i wish it was, because it would've been clever), 
the so-called Interface Segregation.

Interface Segregation calls for small, composable interfaces that only include methods absolutely
needed for one specific task. In a way, Interface Segregation is Single Responsibility Principle
applied to interfaces.

Problem is, it usually isn't applied. Most codebases rely on large interfaces, full of completely
or at least not directly related methods that could easily be segregated into separate interfaces.
And there's quite a bit of value in doing that - it lets your IDE tell you you're an idiot for
trying to push an item into a readonly collection, for example.

## Java Collections framework

I can't claim this about all the languages, but i certainly can confidently state that
Java's collection framework *sucks*, it really does.

This is where this insight originated.

No, not the implementation - the implementation is decent, i can't say i've ever encountered
a performance problem that was rooted in how these collections are implemented. Nor have i 
encountered any weird bugs when using these collections, although i do wish their concurrent maps 
supported null values. Also, maybe i just don't have enough experience to have found enough
bugs to write a three-pages rant about this framework.

But i do have one, quite major, complaint.

The framework is built around a set of very useless interfaces. Monolithic interfaces that
carry with them so many unnecessary methods, that it's just silly. If i want to push to a collection
my client passed me, do i really need to accept a Queue with all of its other methods?

On one hand, me, who's writing the method accepting a Queue, is tempted to use all of Queue's
methods, even if that might not be logically correct.

On the other hand, the user of my API is forced to implement Queue completely, even if it
makes zero sense to do so.

## Sometimes C# isn't much sharper

C#'s situation is *slightly* better, but still far from ideal. There are more interfaces, which
is certainly nice - but they are still quite bloated and monolithic, forcing you to care
about methods that just don't matter to you.

## Why don't you just implement the interface and forget about it?

If i need to explain to you just how stupid the concept of an ``UnsupportedOperationException``
is, then, well, i give up.

I do not want to implement methods i don't need to implement, and i especially don't want to
implement them as NOOPs or, better yet, ``UnsupportedOperationException``-throwing runtime-landmines.

## The ultimate reason behind it all...

...is that these two languages do not natively support type unions.

Honestly. I believe if they supported the notion of ``IPushable&IPoppable&IIndexed<int> list`` or
something along those lines, the programmers would be just that much more confident to actually
segregate their humongous interfaces into small, composable pieces.

Which, i suppose, is another insight - why don't C# and Java support such interface unions? It
seems like a pretty easy thing to implement, certainly easier than generics.