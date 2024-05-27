---
title: "Use .mailmap for Name Changes on Git"
date: 2021-05-23T11:56:15-04:00
cover: "hello-my-name-is.png"
useRelativeCover: true
draft: false
---

FIXME: small edit for change

Whenever we change a name, git tracks a different author. The
following names are all different authors insofar as git is
concerned:

- Quintessence
- quintessence
- Quinn
- quin

Similar applies if you are using different email addresses, e.g.
different personal addresses or different work / contract
addresses. And then of course there are situations where people
legally change their names, for a variety of reasons like
transition, marriage, severing ties with family of origin, etc.

# When Two (Or More) Become One

In order to tell Git that these different authors are one,
standard, author you use the `.mailmap` file. To show by example,
let's say that you need to make the following changes:

- An Alexandra to Sasha, same email of `sasha@email.com`
- A Hana Doe to Hana Smith, same email of `hana@email.com`
- A Jayne Cobb to George Parley, different email of the same
  pattern `firstname@email.com`
- Janet, same name but email from `janet@email.com` to
  `notagirl@email.com`

In this initial example, all the emails will stay the same, so I
have some placehodlers. The way you would structure your `.mailmap`
file would be:

```
Sasha <sasha@email.com>
Hana Smith <hana@email.com>
Jayne Cobb <jayne@email.com> George Parley <george@email.com>
Janet <janet@email.com> <notagirl@email.com>
```

You can see in the above that names or emails are matched, so you
don't need to specify the redundant information (e.g. `Alexandra
<sasha@email.com> Sasha <sasha@email.com>`).

You can still also resolve the initial example I gave of variants
of my own name, by just doing one line (assuming I'm using the
same email for a given repo):

```
Quintessence <quintessence@email.com>
```

That would resolve all the Qs, Quinns, Quins, and Quintessences,
as well as any case variants, to `Quintessence`. A similar step
would resolve any email disparities if I also had various emails
from changing email addresses over time.

## Getting Started

If you are generating your first `.mailmap` file and you have more
authors than you know what to do with, for example if instead of
cleaning up your own repos (hi) you're cleaning up company repos, 
then you can generate your initial `.mailmap` with:

```
git shortlog -se > .mailmap
```

The output of that command will look something like:

```
   21	Quintessence <quintessence@email.com>
```

You'll need to clean up the first part, which is the number
of commits associated with each author. If you'd like to use
`vim`, and I do, you can do this by going into the `vim` editor
and running:

```
:%normal 2dw
```

Breaking that down:

- `normal` runs the command in Normal mode (i.e. runs the command)
- `%` applies it to every line
- `2dw` **d**eletes two **w**ords

[Test]( {{ < ref "vim-getting-started" > }}
