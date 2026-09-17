# One-time setup

Getting this site online and private. Everything here is clicking through
two websites — there is nothing to install and no code to write.

Budget about 20 minutes. You do this once.

> Cloudflare changes its menu wording from time to time. If a button name
> below does not match what you see, look for the closest equivalent — the
> order of the steps does not change. If you get stuck, tell me exactly what
> the screen says and I will work out where it moved to.

---

## Part A — Put the site online (about 10 minutes)

At the end of Part A the site is live but **publicly reachable** by anyone
with the exact URL. Part B is what closes that. Do them in one sitting.

1. Go to **dash.cloudflare.com** and create a free account. Confirm your
   email when it arrives.

2. In the left-hand menu, find **Workers & Pages**, then click **Create**,
   and choose the **Pages** tab.

3. Choose **Connect to Git** and authorise Cloudflare to see your GitHub
   account. When GitHub asks which repositories to grant, you can safely
   pick **only** `InvestmentNews` rather than all of them.

4. Select the `InvestmentNews` repository, then **Begin setup**.

5. On the build settings screen — this is the part that looks alarming and
   is actually trivial. This site has no build step, so:

   | Setting | What to enter |
   | --- | --- |
   | Production branch | `main` |
   | Framework preset | `None` |
   | Build command | *leave completely empty* |
   | Build output directory | `/` |

6. Click **Save and Deploy** and wait. It takes under a minute.

7. You will get a URL ending in `.pages.dev`. Open it. You should see your
   briefing page exactly as it looks today.

**Paste that URL into `README.md`** under "Live site" so we both have it.

---

## Part B — Put a login in front of it (about 10 minutes)

This is the step that makes the site actually private.

1. In the Cloudflare menu, open **Zero Trust**. The first time, it asks you
   to pick a team name — any name, you rarely see it again — and to choose a
   plan. **Choose the Free plan.** It may ask for card details to verify you;
   the free plan for one user does not charge.

2. Go to **Access** → **Applications** → **Add an application**.

3. Choose **Self-hosted**.

4. Give it a name (`Tech Investment Scan`) and point it at your Pages site.
   Cloudflare usually offers your Pages project in a dropdown — pick it. If
   it asks for a domain instead, enter your `.pages.dev` address.

5. Add a policy:

   | Field | Value |
   | --- | --- |
   | Policy name | `Just me` |
   | Action | `Allow` |
   | Include → selector | `Emails` |
   | Value | your own email address |

6. For the login method, make sure **One-time PIN** is enabled. That means
   Cloudflare emails you a code — no password to remember, no extra account.

7. Save.

### Check it worked

This matters more than it sounds — a login you have not tested is not a login.

1. Open your `.pages.dev` URL in a **private/incognito window**.
2. You should be stopped by a Cloudflare login screen, not the briefing.
3. Enter your email, get the code, paste it in, and the briefing appears.
4. Now try it with a *different* email address if you have one. You should
   be refused.

If step 2 shows you the briefing straight away with no login screen, the
policy is not attached correctly — tell me and we will fix it before going on.

---

## Part C — The spending cap (do this at step 4, not now)

You do not need this until we add the AI commentary, but noting it here so
it does not get forgotten.

When you create an API account for the writing step, **set a hard monthly
spending limit in the billing settings before using the key**. Expected spend
is $1-2/month; a cap of $10 leaves plenty of headroom while making a runaway
bug impossible to feel. This is the single most important guard rail in the
whole project.

Also: the API key goes in **GitHub → Settings → Secrets**, never in a file
in this repository. `.gitignore` is set up to help, but the rule is simply
never to paste a key into a file here.

---

## After setup

From this point on, changing the site means editing a file in this repo and
pushing. Cloudflare notices within seconds and republishes automatically. You
never touch the Cloudflare dashboard again unless you want to change who can
log in.
