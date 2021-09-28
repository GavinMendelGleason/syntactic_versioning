# Does Git Dream in Text?

Quite a few people [commented in a discussion on Hacker
News](https://news.ycombinator.com/item?id=28670372) regarding my
position piece [What if Git worked with Programming
Languages?](./README.md) stating that I'm wrong - that Git doesn't
actually do anything with lines. I knew that when I wrote the piece
that this objection would arise, and was a bit unsure of whether to
deal with it in the piece or not.

In the end I decided against mentioning it.

The reason for doing so is that the vast majority of users of git
*know* that git thinks in lines of text. How could anyone think
otherwise? The git commands constantly are alerting you about changes
in terms of lines of text, git has a built in diff command and many of
the operations end up being the application of patches which are in
fact lines of text. The programme interface structured in such a way
that the git users experience is precisely about lines of text.

There are a few cognoscenti on the other hand who *know* that git is
*not* storing changes to lines of text. This is actually very relevant
to the *model* of git storage because other revision control systems
in the past really *did* store [diffs as the primary
quantum](https://en.wikipedia.org/wiki/Source_Code_Control_System). Git
instead stores collections of hashes which are content addressable to
entire snapshots. This is a very different, and arguably better,
model.

Or at least arguably better if what you're doing is comparing lines of
text.

## Storing Structure

Full disclosure: I'm a member of the engineering team which developed
[TerminusDB](https://terminusdb.com/), a version controlled graph
database. When we were designing the architecture, we used git as sort
of north-star to understand the *best* way to do version
control. Having used other version control systems, I wanted to avoid
some of the pitfalls.

However, while many elements of the storage mechanism in git turned
out to be useful and instructive, the fact that it stores file objects
each as their own thing proved to be less than ideal for the use-cases
we envisaged. We wanted to be able to store database structure and
retrieve *fragments* of previous states of the database quickly by
querying them. With large amounts of queryable data it makes a lot
more sense to use a [persistent data
structure](https://en.wikipedia.org/wiki/Persistent_data_structure),
rather than a check-pointed dump.

And a graph database is nearly ideal for storing ASTs. TerminusDB uses
the idea internally to store the [query
language](https://github.com/terminusdb/terminusdb/blob/main/src/terminus-schema/woql.json).

These aren't just text files after all.

## Different Diffs

As some people also mentioned, git *does* expose the ability to do
different types of diffs. This could, in theory give you the ability
to do structural diffs inside of git, given that you knew something
about the syntax of the object you were working with.

However, how do you make a tool that doesn't know anything about the
syntax of the objects with which you are dealing *a priori*. In this
case you need to have a system which is able to perform diffs on
[generic ASTs](https://www.andres-loeh.de/GDiff.html). Plus, you will
need to be pushing the AST generation further up the chain. This
allows you to generically support any language that can be represented
as an AST (I learned on the HN thread, that *perl*

## So Text it is

And here we are back to the fact that git is designed to work with
text files. It is not meant for *storing structure*, *querying
structure* or *diffing structure*.

That isn't a bad thing. It's just because of what git was designed
for. As an excellent tool for tracking changes in text files.
