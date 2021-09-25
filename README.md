# What if Git worked with Programming Languages?

I use git most days of the week. And for the great majority of my
commits, this means committing.

So why would I say something like *What if Git worked with Programming
Languages*?

Well, the title is deliberately provocative, but I genuinely mean it,
and it's not wrong: Git does *not* work with programming
languages. Instead it works with source files of text.

## A Potted History of Version History

I absolutely love git, and I love what it has done to the
development process even more.

I remember the bad old days of revision control. I used *file* based
revision control on VMS. I've used CVS, subversion (svn), and visual
source safe in development environments. The pain and torment these
systems caused me has been quite successfully sublimated into my
unconscious mind, only rising to the surface when I'm forced to think
about the history of revision control.

Git is not without its pains - you'll find yourself knee deep in some
horendous merge or rebase at some point, confused how to get things
working again. But there are so many benefits over what it was like in
the past that these things are easily excused.

The fundamentally multi-master approach of git, combined with the
concepts of CI/CD have yielded enormous benefits. They've actually
made my life better.

But they've also made collaboration better. I'm still learning about
the potential to improve software develpment on a nearly weekly
basis. In my opinion the well of possibilities in most development
houses is probably not yet fully tapped.

Automatic testing, including unit tests or even very sophisticated
integration testing becomes enormously simpler with the ability to
create the *hypothetical commits* of a pull request. It's essentially
like having a [modal
logic](https://en.wikipedia.org/wiki/Possible_world) at our disposal
for reasoning about correctness.

Yet it would be hubris to think that this is the the end of history
for versioning.

## Git for programming languages

The fact that git works on *lines of text* has worked fantastically
well - better than it has any right too. But then our programming
language editors are also designed as *text editors*, so maybe this
shouldn't be too surprising.

The text orientated design reflects the old unix philosophy of
creating simple tools that work generically. And for unix generic
meant files and text (think sed, awk, pipes etc).  Git builds on
technology that literally goes back to the beginning of unix, the
`diff` program.

In *fact* the current version of git is also able to find differences
in binary files. But this eschews lines of text for continuous
strings. This does not represent a *greater* awareness, but rather a
*lesser* awareness of the *syntax and semantics*.

But programming languages are not really just lines of text. Diffs
from two different changes to a source file are not necessarily
composable, even if there are no overlapping changes. Program code has
syntax, and this syntax is knowable, even in the case of the most
dynamic of languages (such as those with configurable readers such as
Common Lisp).

We should be able to leverage this. Or rather we *should* leverage
this. When we do a diff between two different source programmes, we
*could* be looking at the alterations to the [abstract syntax
tree](https://www.andres-loeh.de/GDiff.html). And these diffs can even
be found and applied
[efficiently](https://dl.acm.org/doi/10.1145/3341717).

And if we were storing information as ASTs, rather than lines of text,
we could store them in a [graph
database](http://terminusdb.com). Imagine the kinds of testing and
linting which could now take place. You could have a full graph query
language at your disposal to search for problems and perform analysis!

Of course the *unit of analysis* for programming languages has
remained the text file. [Structure
editors](https://en.wikipedia.org/wiki/Structure_editor) haven't
really yet taken off despite several
[historical](https://larrymasinter.net/interlisp-ieee.pdf) and
[contemporary](https://github.com/JetBrains/MPS) examples. There are
probably good reasons for this. Humans expect things that they saw
recently adjacent to remain spatially adjacent. Files definitely act
like this, whereas the SmallTalk approach of putting it in a database
does not. However we don't have to abandon this structure to also get
the benefits of structure editors. Lists also retain order and
adjacency. There is also the problem of what to do when in a
syntactically invalid state. But there are ways around this (think
commit) and some programming environments, (such as
[agda-mode](https://agda.readthedocs.io/en/v2.6.0.1/tools/emacs-mode.html))
are good at it.

Editors could really leverage a whole universe of new possibilities if
they were storing structured documents at commits, rather than merely
source files. And if you're worried that you need to put some code
somewhere and you don't know what it is yet, see
[holes](https://jfdm.github.io/post/2020-07-09-Programming-with-holes.html).

And as code bases grow, the need for more sophisticated linting, for
better approaches to search and retrieval, for looking at all callers,
etc. becomes more important. What could be done with grep and a few
text files ceases to be pragmatic when your source tree is several
hundred thousands or even millions of lines.

It seems to me that there are real advantages to going beyond the
"lines of text" view of programming languages.

## The New (and Old) Data Science Tools

But while there may be advantages as yet unexplored for languages like
python, there is a new class of very widely used *notebooks* such as
[Jupyter Notebooks](https://jupyter.org/). These tools are
intermediate between analytic environments and programming
environments. They store graphics, data and program code together in a
way that the outcomes can be easily reconstructed. This is a big
advantage in data-science where you want to share your results. It is
one of the reasons that JetBrains developed its MPS
structure-editor. It was to facilitate the creation of domain specific
languages which could likewise have rich environments.

And while this new approach to data science feels cutting-edge, if we
look carefully (and squint our eyes just the right way) we'll
recognise that the most widely used [programming language on the
planet, Excel](https://github.com/terminusdb-labs/data_mesh), is one
of these data-visualisation-programming systems.

Unfortunately, because these new notebooks are *richer* than mere text
files, they also fight our collaboration tools. Git is significantly
more painful when working with Jupyter. The more we begin to rely on
these tools for rapid development of data science analytic results,
the more we will need advancement on the collaboration and CI/CD
front.

## Conclusion

Git's power and advantage over older collaboration and revision
control tools is clear, but is this the end of the story? I wager it
isn't.

The future will be in structured storage, structured diff, structured
linting and search and perhaps someday we will finally get our
structure editors.
