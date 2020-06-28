# Elite Task Force Lambda

...is here to make your life immutable.

This insight is a WIP. It's flow may be awkward, and some of the sections may be incomplete.

## Functional Programming is great. So is Object Oriented Programming.

The two should co-exist.

Both paradigms have their strengths and weaknesses, and, in all honesty, can very nicely
complement each other. OOP brings to the table better performance, ease of customization
(polymorphism!) and the convenience of mutable state; FP instead offers the true 
thread-safe power of immutable data and the criminally convenient function pipelines.

And, indeed, the further we move along in our timeline, the more we see the popular languages
try and adopt features from both paradigms, and make them interop well with each other.

Java and C# are definitely on the OOP side of the scale, but Java has, in the "recent"
versions, received many functional-ish classes - `CompletableFuture<T>` and `Option<T>`, for
example. The Collections framework is also interested in the functional approach, it seems -
and if you decide to stream your collection instead, you suddenly ascend to a new functional 
dimension.

C# has also been getting more and more functional. Probably more than Java, but my experience
with this language is sadly limited to my Unity fiddles, so i am probably missing on some key
changes. Still - delegates(which i believe could count as first-class functions?), lambdas for
class properties(getters and setters), and, most importantly, the grand Linq framework.
Which is kind of like Java's Collections framework, but on steroids, *and* with language-level
support(to the point that the programmer can write SQL-like queries in C# code).

Javascript, on the other hand, was certainly more on the FP side of things. I mean sure,
it had objects, it had this weird prototype-based inheritance, but that's pretty awkward by
OOP standards, and the fact that functions were always first-class and never truly bound to
objects strongly suggests it's a FP language. Or, at least it was, before they ended up
adding classes. Because people wanted classes. Classes can be quite useful, as it turns out -
even in a dynamically-typed language.

I'm sure there are plenty more examples - feel free to suggest more. But case in point is:
OOP and FP can, and *should* coexist.

However, some FP folks don't feel that way.

## OOP is dead, long live FP!

It takes very little effort to find an article with such a title. And not one, but many articles.
OOP is dead, apparently. It "didn't deliver what it promised", it "distracts people with useless
abstractions", it "is merely an illusion of structure and will bite you in the ass down the line".

But is it, really?

I think OOP is perfectly fine and will continue to be used for decades if not centuries.
It's a battle-tested approach that is easy to grasp, incredibly flexible(often too flexible),
and rather intuitive for someone who grew up in a world full of objects(as fuzzy as those may be).

Both of these paradigms are merely tools that are good at solving some tasks, and bad at solving others.

So here i want to address the articles i've read, whose authors seem to be quite keen on the idea
that "pure" FP with no mutable state is somehow a good idea.

It can be. For some tasks. But for most tasks, it's just asking for trouble.

## Objectively straightforward

I do support the notion that OOP is easier to learn for someone that hasn't programmed before.
How much easier? Well, not orders of magnitude probably, but maybe twice or even thrice.
The reasoning is simple - the world is fuzzy, yes, but it is filled with objects, not
mathematical functions. So people can reuse their limited object-oriented experience
when learning OOP languages.

Whether that's a good thing, hard to say. It certainly means you can train developers quicker.
Whether this produces good developers is not something i have a good opinion on. Because yes,
i do buy the idea that FP is more involved and thought-heavy than OOP. This means that it takes
more effort to do anything with it, at least until you gain enough experience, but it also
does imply that the skill profile of all the FP programmers is skewed towards the 
"knows his shit" side.

One could argue that this is merely a fluke, a coincidence, a consequence of the fact that
OOP languages are favored by various universities around the globe, and that the illusion of
OOP being easier is merely a product of this assymetric allocation of educational resources.
To that, i also say "fair enough." 

Maybe that is the case. In which case, do you know how to fix that? I certainly don't.
And if you do, trust me, you could do so much more for this world than just teach it FP.
Being able to meaningfully and heavily refactor the education system is a superpower that
could turn our civilization from a doomed hellfire into a galactic empire.

But shitting on OOP isn't the way to do it.

## .replace() instead of .remove()

OOP sucks! Stop using OOP! You're doing OOP wrong! OOP is a waste of resources!

Okay. What are you proposing we use instead?

The articles i've read lately all seem to follow this implicit script of "guys, OOP
is a bad thing, don't use it. Use FP. Trust me. In my experience, it's been great!"
I'm happy that your experience with it has been outstanding. However, that sort of
a sentiment provides very little motivation for me to start using FP. (We'll ignore
the fact that i use FP very often in OOP languages, for this part.) If you want to 
change someone's opinion or anything, you don't just need to defeat their current
opinion, you also need to show that the opinion you are attempting to push into their
head is actually better.

And i don't mean abstract crap. Abstract crap is abstract. Programmers are engineers,
not philosophers.

Show me concrete examples. Show me games written in FP, or better yet, pure FP - 
and show me how you dealt with the performance issues. Show me a full-on REST API
server with heavy and highly conditional logic underlying its endpoints - and show
me how you encoded the relations between its modules as functions, and how you turned
imperative logical flows into declarative function call trees. Show me other remarkable
achievements of FP - things that are, at first glance, doable in OOP and OOP only,
but nevertheless clearly benefit from being rewritten in a more functional way.

## The Three Pillars

### The Vault Skyscraper of Hidden State

The pillar of Encapsulation provides quite a bit of good. Data that is hidden and managed
by the object, in clearly defined and (hopefully) well-tested ways. This, at least to some
extent, provides some guarantees about the validity of our system's state in our mutable,
multithreaded environment.

Of course, there's always that one time when the object is just not cooperating, or
is just straight up stupid about managing its belongings. And that's when the programmer
sighs and either A) writes their own object instead, B) copies the source of the object in question
and fixes the broken crap, or C) grabs the sword and shield of Reflection and dynamically
interacts with the protected fields.

Which isn't a good thing, in my opinion. I, as a client of your code, am grateful that you
hid your implementation details from me, so that i don't need to think so much about which
methods and fields i am safe to access. But i do believe this should be a suggestion, not
an enforced rule - because if i, as a client of your code, decide that i *really* need to 
edit your object's internal fields, and i have a *really good reason to*, i should be allowed
to do it. Without inheritance, low-performance dynamic dispatch and other ugly crap.

So i think in general Encapsulation is a good thing, but its implementation in most languages
could be better.

### The Obelisk of Abstract Classes

The pillar of Inheritance never really supported anything. Hell, it isn't even a pillar.
It is an obelisk in memory of all the wasted resources that were lost in the misguided effort
to Reuse code via, well, Inheritance.

Inheritance is a better-than-nothing solution to the problem of code reuse. But i am
certain there are better ways. Ways that don't lead to the diamond problem, nor 
create deep Inheritance dependencies, nor force you to inherit the functionality that
you don't care about.

So i'll be the first to admit - Inheritance *was* a mistake, and OOP suffered from it greatly.

### The Colorful Tower of Interfaces

The pillar of Polymorphism is undoubtfully the most useful of the three. Being able
to substitute objects and not rewrite your code is surprisingly helpful, and it speeds
the development and makes the system more flexible.

## The gameplay element

I'm sure there are games written in a FP style. I can't imagine there being more than
a couple of games written in *pure FP* style, with no mutable state and copying of
data on every step, but i imagine it's possible.

But as for OOP? Well, it's pretty much in every game. At least nowadays - i suppose
back in the day more games were written in a procedural style, but eventually the
objects won out.

I think the reasons are pretty simple. 

### The Emergent Keyboard

An often-cited counterargument to OOP is that objects cannot truly model our fuzzy world
in a meaningful way. That's debatable, but even if it is true - videogames usually don't want
to model a fuzzy world. That's just asking for trouble. The more possible interactions there
are, the more detalization, the fewer clearly concepts - the more work you'll need to put
in to get anything done. A videogame simulating our universe by solving atom-vs-atom interaction
is theoretically a possibility, but is a stupid idea even if you do somehow magically have the 
computational resources to run it at a decent framerate.

Why? Well, because, for example, me personally couldn't give less of a shit if the keyboard in 
front of me actually consisted of atoms, or merely acted as if it did. If it shows the same
emergent behavior as would a proper keyboard actually consisting of atoms, then i don't mind.

As such, it is an *object* with *methods*(behaviors) and *properties*. It can probably do
several things, and to make it do these things you need to interact with it in a specific way -
you need to use it's *interfaces*.

You probably could model this via FP. I don't see how, but then again i'm not the FP guy around 
here. I would imagine it would require quite a bit more abstract thinking and mind-twisting 
confusion than the OOP approach does - so much for unhelpful abstractions. Hey, if you know
of a way to meaningfully model the concept of a keyboard in a pure FP fashion, do let me know.

### Carbon Copy

But the even more problematic thing about using pure FP for gamedev is performance.

Yes. Immutable objects passed by-value to every consumer are nice. They are absolutely
thread safe and ensure there are no side effects. But the thing is, copying takes effort.
Not a lot generally, but each copy adds up. One of the reasons we like to use mutable
states this much is because, while they are a source of threading and action-at-a-distance
issues, they are *performant*. You don't need to handle the entire object if you
only want to modify one field - you just modify the field. 

You can, of course, use mutable state in your FP language, and then things kind of settle
down. I still think the FP approach is not viable for representing the abstract 
and very-well-segregated world of videogames, where objects are full of objects and interact
with objects. But it does make the situation tolerable. It also provides me with an argument
i can use to counter people who claim that the "true", "pure" FP powered by immutables
and immutables only is the only true way to program things.

No, it is not. Mutability is a good thing. Immutability is a good thing. The amount of
goodness varies. You are the programmer - your job is to weigh these tradeoffs and
choose wisely.

Religiously sticking to one or the other is a sign of a bad programmer.

## The conclusion

The way forward isn't religious and elitist crap-carpet-bombing of OOP as a concept.
It has its flaws, it has its weaknesses. Most of its problems come from the implementation.
The few that are rooted in the paradigm can be worked around, and often with the use of FP.
That is no valid ground to drop OOP completely.

The way forward is to mix the two. Use each situationally, and put effort into making their
interop smooth and enjoyable. Encourage people to learn FP, and encourage the people behind
OOP platforms to improve their platforms, adopt new ideas and drop the outdated ones(Inheritance
must fall).

OOP will handle the abstract modular graph of the system as a whole, the high-level structure
and connection between modules. FP will power these modules. That is probably the future we're
headed towards, and it is a good future.