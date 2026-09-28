# MYMINI164

A collection tracker for 1:64 scale diecast model cars, at
[mymini164.com](https://mymini164.com).

Record what you own, what you have on order and what you are still looking for, across a
catalogue of tens of thousands of releases from more than twenty makers' catalogues —
Hot Wheels, Tomica, Mini GT, Tarmac Works, Time Micro, PARA64, Inno64, Pop Race,
XCarToys, Schuco, IXO, Era Car, BBR, Sparky, Kyosho, Bburago, Majorette, Almost Real and
others — with photographs, product codes, barcodes, regional exclusives, release dates,
set contents, rarity and provenance.

No exact figures here on purpose. The catalogue grows most weeks, and a README that has
to be edited every time it does is a README that is wrong most of the time. The
application says what it holds, on its own sign-in screen, worked out from the catalogue
it was built with.

## Your collection

Your collection starts **private** and stays private until you decide otherwise. There is
a community: other collectors can find your profile, follow you and ask to be friends,
and you choose whether any of them can see what is on your shelf — private, friends only,
or open to signed-in members. What you paid is never shown to anybody under any setting.

All of that is enforced in the database by row level security and by functions that check
who is asking, not by what the page chooses to draw. A request for something you are not
entitled to is refused whoever makes it, including from outside the application.

See the [privacy notice](https://mymini164.com/privacy.html) for who can see what, what is
stored, the lawful basis for each kind of processing, and which companies are involved.

## How it is put together

One generated HTML shell, with the application fetched as a hashed script after sign-in
and the photographs served as individual WebP files beside it. There is no server of its
own: accounts and collections live in Supabase, which the page talks to directly, and the
static files are served by GitHub Pages.

The key in the page is a **publishable** key, which is what a publishable key is for.
It grants nothing on its own: every table refuses an anonymous read, and every row a
signed-in collector can reach is decided by row level security in the database.

Nothing here is hand-written. `hosted.py` builds all three shapes — the offline copy, the
published single-owner copy and the multi-user application — from one source and one set
of catalogue files.

## Caching

The application script is named after a hash of its own contents
(`p/app-<hash>.js`), so a new build is a new filename and an old one can never be served
in its place. That makes it safe to cache for a year. GitHub Pages does not let a site
set its own cache headers and serves everything with a short max-age, so the long cache
is not in effect today; the filenames are already right for it, and putting a CDN in front
of the existing deployment would switch it on without moving anything. `_headers` in the
published output carries that configuration, ready, for any host that reads it.

## Contributing

The catalogue is compiled from manufacturers' own listings, official catalogues, licensed
distributors, specialist retailers and collector databases, in that order of preference,
and every row records where it came from and how sure that source is. If you find a
release that is missing or a row that is wrong, "a missing car" and "report a problem"
inside the application are the way to say so.
