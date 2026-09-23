# Mini164

A collection tracker for 1:64 scale diecast model cars.

3,901 catalogue entries across Mini GT, Tarmac Works, PARA64, Pop Race, XCarToys,
Schuco and BBR, with 3,686 photographs, barcodes, regional exclusives, release dates
and set contents.

Sign in and the collection you build is your own. Nobody else can see it or change it.

## How it works

The whole application is one HTML file with the photographs beside it. There is nothing
to build and no server of its own. Accounts and collections live in Supabase, which the
page talks to directly.

The key in the page is a publishable one, which is what publishable keys are for. Every
row is protected by row level security in the database rather than by the page, so a
signed-in person can read and write their own collection and nothing else. The catalogue
itself ships owned by nobody.

## Running it

It is a static site. Serve the folder over http and open it:

    python3 -m http.server 8080

Opening `index.html` straight from disk half works: the sign-in appears, but a browser
will not let a page opened from a folder read the photograph files next to it, so every
card comes up blank.
