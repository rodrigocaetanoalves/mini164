Mini164, the version with accounts
==================================

This folder is the whole application: one HTML file and the photographs. There is
nothing to build. Accounts and collections live in Supabase (project Mini164, London),
which the page talks to directly.


DO NOT JUST DOUBLE-CLICK index.html
-----------------------------------

It half works, which is worse than not working. You get the sign-in screen and you can
probably create the account, but:

  - none of the 3,686 photographs load. A browser refuses to let a page opened from a
    folder read other files next to it, so p/photos_*.json is blocked and every card
    either sits blank or goes off to the shops one image at a time.
  - a password reset email would send you back to a file:// address, which is not a
    web page anybody can open.

Use one of the two below instead. Both take a minute.


1. TO TRY IT RIGHT NOW, ON THIS MAC ONLY
----------------------------------------

Open Terminal and run:

    cd ~/Desktop/DieCastCollection/mini164-site
    python3 -m http.server 8080

Leave that window open, and go to:

    http://localhost:8080

That is a real web address as far as the browser is concerned, so everything works:
photographs, sign-in, your collection, the lot. python3 already comes with macOS.

Create your account here with rodrigo.private@outlook.com and your collection attaches
itself on the spot. The account is real, on the live database, so when you put the site
online later you sign in at the new address with the same password and everything is
already there. Nothing has to be done twice.

Press Control-C in Terminal to stop the server. Only this Mac can reach it.


2. TO PUT IT ONLINE FOR YOUR FRIENDS
------------------------------------

Same folder, one command:

    npx wrangler pages deploy . --project-name mini164

The first run asks you to sign in to Cloudflare in the browser and makes the project for
you. It prints a URL like https://mini164.pages.dev, and that is the link you send
people. Running it again publishes an update.

Cloudflare Pages because its bandwidth is unlimited on the free plan and this folder is
34 MB of photographs. Netlify and Vercel work the same way
(`npx netlify deploy --prod --dir=.`, `npx vercel --prod`) but both meter bandwidth, and
a handful of testers at 34 MB each would eat a free allowance quickly.

Tell me the URL afterwards. One Supabase setting needs it: the address password-reset
emails send people back to. Until that is set, reset links point at wherever you last
used the app, so a link generated from localhost only works while that server is running.


YOUR ACCOUNT
------------

Use rodrigo.private@outlook.com. Your collection is waiting under that address and
attaches itself the moment the account is made: 295 cars, 232 owned, 55 on the way, 4 on
the want list, 26 orders, every price, shop and note. That account is also the
administrator. Any other address gets an ordinary empty account, which is what your
friends get.

The password is yours alone. It is never in the chat and is never stored anywhere except
as a hash inside Supabase's own auth service.


BEFORE YOU INVITE MORE THAN ONE OR TWO PEOPLE
---------------------------------------------

Supabase's built-in email is rate limited to a few messages an hour. That covers you and
a friend, not ten. Password resets go through it. Connecting a real sender (Resend and
Postmark both have free tiers) is about ten minutes in the Supabase dashboard, under
Authentication, SMTP Settings.
