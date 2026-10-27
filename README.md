# Tutorial — Customize Your GitHub Profile README (a Real Case: Mine)


## What you will learn

By the end of this tutorial you will be able to:

1. Explain how GitHub decides to render a README on your profile, and create the special repo in under two minutes.
2. Build the static pieces (badges, icon grids, native Markdown sections) with copy-paste code you can trust.
3. Add data cards automated with GitHub Actions, knowing in advance what breaks, when, and why.
4. Decide what to add and what to skip, weighing security, privacy, and the actual evidence (thin) on whether any of this helps your career.

---

## The two-minute trick: a repo named after you

GitHub renders a README on your profile when a public repository exists whose name exactly matches your username and that contains a non-empty `README.md` at its root. All three conditions are evaluated together: make the repo private, empty the file, or rename it, and your profile goes blank again. That is the whole mechanism. There is nothing else to configure.

To create it: on github.com, click `+` → **New repository**. Name it exactly as your username (mine is `Jesus-Valverde`). Set it to **Public**, tick **Add a README**, and create the repo. GitHub detects the special repo and offers an **Edit README** button right on your profile.

Three exceptions that surprise people:

- Managed accounts (provisioned by a company through GitHub Enterprise Managed Users) cannot have a personalized profile; the official documentation excludes them explicitly.
- If you created a repo named after you before July 2020, it does not show up automatically: open the repo and press **Share to profile**.
- The official documentation URLs were reorganized in 2025, so many older tutorials link paths that now redirect. The content is still there; the link is what aged.

A note on achievements: there is a rumor that GitHub removed them. What is verified as of October 2026 is different: the achievements documentation page returns a 404, two badges can no longer be earned, and users report badges frozen since 2025. But there is no official retirement announcement, and badges like Pull Shark are still listed as earnable. If a tutorial dangles them as a goal, treat them as unstable garnish.

## My profile, on the operating table

This tutorial was born from a real pending item: my profile has a section that says "👉 Tutorials", shows a "loading..." GIF, and admits it is unfinished. What follows is the anatomy of what I already built, with the good, the fragile, and the missing.

My `README.md` weighs 3,369 bytes and has this structure: a greeting, the Tutorials section (the placeholder), a "who am I" section with the Mexican flag, another on my studies, a row of 11 technology badges, 3 buttons to practice platforms (freeCodeCamp, Exercism, HackerRank), 3 contact buttons (LinkedIn, Linktree, email), and a card from my Steam profile. That is 17 badges in total, all served by shields.io with the `for-the-badge` style.

Each badge follows this pattern (the real one, copied from the file):

```markdown
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
```

What my README gets right, without having planned it: every image has alternative text (`alt`), I use `<br>` to control line breaks, and sections use proper `##` headings. That makes it readable for screen readers, which is exactly what GitHub's own accessibility guidance recommends for profiles.

What it was missing: statistics cards, a contribution streak, and the famous snake. And two fragilities I will point out with the same candor: my Steam card is served by a community service (`card.yuy1n.io`) with no backing; if that service dies, the largest block of my profile breaks. And the email button uses a `mailto:` link with my Gmail in plain sight, which spam harvesters read with pleasure. We will cover the locks further down.

## The badge factory: shields.io

A badge is an image generated on demand from its own URL. The basic shields.io format is `img.shields.io/badge/LABEL-MESSAGE-COLOR`, and most of the power lives in the query parameters: `style` chooses among `flat` (the default), `flat-square`, `plastic`, `for-the-badge`, and `social`; `logo` takes the name of any icon in the simple-icons catalog; `logoColor` and the badge color accept hex.

Three escaping rules cause 90% of broken badges: the hyphen `-` separates segments, so a literal hyphen is written `--`; a literal underscore is written `__`; and the `#` of hex colors is encoded as `%23` (a bare hex without `#` also works).

To make a badge clickable, do not use the `link=` parameter (it does not work inside `<img>`); wrap the Markdown image in a normal link:

```markdown
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/your-username/)
```

On service limits: shields.io publishes no per-client quota figures. What its tracker reports is that real limits usually come from the external service the badge queries, not from shields itself. If some blog gives you an exact requests-per-minute number, be suspicious: it is not documented.

## Icons without text: skill-icons

A compact alternative to badge rows is skill-icons: a single URL that draws a grid of rounded icons.

```markdown
[![My Skills](https://skillicons.dev/icons?i=js,html,css,react,py,flask&theme=dark)](https://skillicons.dev)
```

Ids are lowercase slugs (`js`, `py`, `react`, `nextjs`, `kubernetes`...), the default theme is `dark`, and `perline` controls icons per line (1 to 50). The tradeoff: with no text next to them, a wall of logos is less legible to whoever does not recognize the icons. For a portfolio profile, named badges communicate better; compact icons win when the list is long.

A 2026 detail: the original project (tandpfun) is alive but slow, with over a thousand issues in the queue. A more active community alternative exists, `skills.syvixor.com`, with over 1,059 icons and a real advantage: it adapts to light/dark theme automatically based on the visitor's preference. That fallback proved necessary the very day I published this tutorial: skillicons.dev has no icons for React Router or JWT (it returns empty squares, with a misleading HTTP 200), and syvixor has both under the slugs `reactrouter` and `jwt`.

## One README, two languages

If you want to offer your profile in more than one language, the canonical pattern (from jonatasemidio's multilanguage-readme-pattern repo) fits in one line: a row of language badges at the top of the README, each one linking to its variant.

```markdown
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)
```

The file convention is a language suffix at the root: `README.md` as the primary and `README.es.md` for Spanish. Every version carries the same badge row, so readers can hop between languages from any of them. The honest limitation: GitHub only renders `README.md` on your profile page (it does not run JavaScript, so there is no "on-site" language switch). The switcher on your profile leads to the repo, where the full version in the other language does render.

## What GitHub gives you for free

Before installing anything, use the native format. GitHub supports collapsible sections, callouts, footnotes, and a tag for theme-switching images. All of it with no external services, no tokens, no maintenance.

Collapsible section (useful so you do not flatten your visitor with text):

```html
<details>
<summary>My journey in detail</summary>

Content goes here. Note: there must be a blank line after `<summary>`
for the inner Markdown to render.

</details>
```

The callouts (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) are written inside a blockquote. The official documentation asks for moderation: at most one or two per document, and only for crucial information. One honest caveat: these callouts render on github.com; on other viewers they degrade to a plain blockquote.

And the most underrated native trick, the image that changes with the visitor's theme:

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner-dark.svg">
  <img alt="Welcome banner" src="banner-light.svg">
</picture>
```

## Header effects (use them sparingly)

If you want a header with presence, the two standard tools are capsule-render, which generates animated SVG banners, and readme-typing-svg, which simulates text typing and deleting itself.

```markdown
![header](https://capsule-render.vercel.app/api?type=wave&color=gradient&height=200&section=header&text=Your%20Name&fontSize=42&animation=fadeIn)

![typing](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=22&pause=1000&multiline=true&width=600&height=80&lines=Web+developer;Learning+Flask+and+React)
```

The `multiline=true` parameter (added in 2025) stacks several phrases separated by semicolons, instead of retyping everything on one line.

The fine print: every effect is one more external dependency, decorative GIFs weigh megabytes, none respects the system's reduced-motion preference, and stacking an animated banner + animated text + GIF + badges gets you the anti-pattern critics call "the profile with 40 animated badges". A practical rule drawn from my own case: my "loading..." GIF works because there is exactly one and it has a narrative purpose. Two more would be noise.

## The data cards

Here lives the heart of the ecosystem: three community services that turn your GitHub activity into image cards.

The statistics card, by anuraghazra (github-readme-stats):

```markdown
![My GitHub stats](https://github-readme-stats.vercel.app/api?username=Jesus-Valverde&show_icons=true&theme=tokyonight)
```

The streak card, by DenverCoder1:

```markdown
![GitHub Streak](https://streak-stats.demolab.com?user=Jesus-Valverde&theme=tokyonight)
```

And the trophy card, by ryo-ma:

```markdown
![Trophy](https://github-profile-trophy.vercel.app/?username=Jesus-Valverde)
```

In the same family as the stats cards there is a fourth one people often forget, and it is the only truly automatic one of them all: the most-used languages card, which GitHub computes from your actual repos (the technology badge row says what you claim to know; this one counts what your code says you do):

```markdown
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Jesus-Valverde&layout=compact&theme=tokyonight&langs_count=8)
```

`layout=compact` turns it into a compact list instead of a percentage bar, and `langs_count` controls how many languages it shows.

Useful parameters on the stats card: `include_all_commits=true` counts lifetime commits (without it, the current year only), `hide_border=true` blends it into the background, and `cache_seconds` controls how long the image is cached (the current minimum is 21,600 seconds, or 6 hours, and the maximum is 86,400, that is, 24 hours; if a tutorial says the minimum is 4 hours, it is outdated).

If you place two cards side by side (with percentage `width`, so they stack on mobile), anchor them with `align="top"`: GitHub aligns images by the text baseline, and since the cards have different natural proportions, the shorter one floats downward. And if you also want them to measure exactly the same, compensate the aspect ratio with the width split. I verified it on my own profile: the stats card measures 467×195 pixels and the streak card 495×195; with `width="48%"` and `width="51%"` the rendered heights match to the pixel, and being percentages they stay matched at any window size.

Now, the problem no silent tutorial tells you about: the hosted instances share GitHub's anonymous API quota, and that makes them intermittent. The project's official discussion (September 2025) ended with a clear recommendation from the team itself: deploy your own instance on Vercel with your own token. The process takes about 15 minutes: fork the repo, connect it to Vercel, and in Vercel's environment variables add `PAT_1` with a classic Personal Access Token (PAT, the access key GitHub uses to authorize programs) with no scopes checked. Then change the card URL from `github-readme-stats.vercel.app` to your instance's. The streak card documents the same self-hosting pattern; the trophy service is still up as is, stable but without development for a while.

## Beyond the trio

A second circle of popular widgets exists. What decides their robustness is who serves the image when someone visits your profile:

| Widget | Who serves the image | If the third party fails |
|---|---|---|
| Views counter (komarev) | Their server, on every visit | Broken or stale badge |
| Activity graph (ashutosh00710) | Their Vercel, on every visit | Broken image (same risk as stats) |
| Summary cards (vn7n24fzkq) | An Action **commits the SVGs to your repo** | Nothing: the image is yours |
| 3D contributions (yoshi389111) | An Action commits the SVG to your repo | Nothing: committed pattern |
| WakaTime (coding time) | Their API + a daily Action | Empty section or error |

That "committed" pattern is the most robust in the ecosystem: the Action runs in your repo, generates the SVG, and saves it as part of your own repository. The image the visitor loads lives on `raw.githubusercontent.com`, that is, on GitHub, not on somebody else's server that can cold-start at 3 a.m.

Two warnings from the extra circle. The views counter is free but runs on a shared server with limited capacity (it has stopped displaying under load, per its own tracker), and its maintainer honestly describes it as a "tracking pixel": it counts visits approximately because GitHub's cache filters part of the traffic. And WakaTime requires enabling "Display activity publicly" on your WakaTime account and refreshes roughly once a day, because the standard setup is a daily cron.

## The snake: your first automation

The ecosystem's most beloved animation is the snake eating your contribution grid (Platane/snk). Unlike the cards, here the image is generated inside your own repo and saved to a branch named `output`; after that, it depends on nobody.

Create the file `.github/workflows/snake.yml`:

```yaml
name: Generate Snake
on:
  schedule:
    - cron: "0 0 * * *"   # daily at midnight UTC
  workflow_dispatch:        # manual button for testing
permissions:
  contents: write
jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk/svg-only@v3
        with:
          github_user_name: Jesus-Valverde
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

And embed it pointing at the raw `output` branch:

```markdown
![Snake animation](https://raw.githubusercontent.com/Jesus-Valverde/Jesus-Valverde/output/github-contribution-grid-snake.svg)
```

The cost: on public repos, Actions minutes are free, and a daily snake run takes about a minute. But there is a rule that breaks more profiles than people imagine: **if your repo goes 60 days without activity, GitHub automatically disables scheduled workflows.** The quote is literal from the documentation. The cruel part is there is no warning on the README: your snake simply stays frozen on the last generated SVG, and you blame the service when the culprit is the paused workflow. The fix: Actions tab → select the workflow → Enable workflow, and make a commit to reset the inactivity clock.

On pricing, the 2025-2026 landscape changed and it is worth citing it correctly: GitHub proposed charging $0.002 per minute for self-hosted runners, the proposal was **postponed** in December 2025 after community backlash (it is neither in effect nor formally cancelled); hosted runner prices were **cut** by up to 39% as of January 2026; and workflows on public repos remain free. If you read that "GitHub now charges for Actions", the source is wrong.

Another popular automation is lowlighter/metrics, which generates infographics with 30+ plugins. Its shared instance (`metrics.lecoq.io`) exists but is chronically rate-limited, in preview mode; the current path is running it as an Action in your own repo or hosting your own web instance with Docker. Keep in mind several of its plugins are broken by third-party changes (Skyline was discontinued by GitHub, Steam changed its API in 2025). And if you write a blog, `gautamkrishnar/blog-post-workflow` inserts your recent posts between two comment tags in your README, via RSS.

One final technical detail: the Actions runtime is migrating from Node 20 to Node 24 (enforced since June 2026), so if you pin old actions they may stop running. Use recent versions.

## Why is my card stale? The two caches

This is the mystery that confuses beginners the most: you updated your stats and the card still shows yesterday's data. Almost always there are two stacked cache layers, and you should blame both.

The first layer is the widget's own: github-readme-stats' `cache_seconds`, 6 hours by default. The second is camo, GitHub's proxy: every external image in a README is rewritten to a URL on `camo.githubusercontent.com`, and that proxy keeps its own copy of the response. Your card can be stale because of the widget layer, the camo layer, or the sum of both.

The simplest fix is making camo see a new URL: append a throwaway parameter (`&v=2`, then `&v=3`...). It is the classic fix from the project (issue #632, from 2020) and it still works. There is also a `curl -X PURGE` against the camo URL to invalidate a specific image, but use it sparingly: it forces every GitHub user to re-download the image. And do not trust `Cache-Control: no-cache` from the origin: there are documented reports of camo ignoring it for short windows.

A privacy bonus that falls out of this design: since the one making the request to the external service is GitHub's proxy and not the visitor's browser, widgets do not see the individual IPs of your readers. Aggregate volume, yes; identified visitors, no.

## Locks: tokens and what you expose

Three security rules that are not negotiable. First: every tool gets the minimum token. The self-hosted stats instance uses a classic PAT with no scopes (in Vercel environment variables, not repo secrets); Actions that commit to your repo (snake, summary cards, 3D) use a fine-grained token limited to that repo with read-write contents permission, stored as a repository secret; metrics uses a no-scope PAT for public data. Second: a token never goes in the README, in the workflow YAML, or in a commit message. GitHub's secret protection detects `ghp_` and `github_pat_` patterns on push, but do not rely on that alone. Third: if a token leaks, revoke it immediately under Settings → Developer settings; deleting the commit revokes nothing.

And the part almost nobody reviews before publishing: what your README says about you to people who are not your audience. A `mailto:` with your email in plain sight guarantees spam (JavaScript or image obfuscation does not work; harvesters defeat it). A public Steam card exposes your library, your playtime, and your friends list. View counters collect telemetry from your profile. None of these is wrong by definition; all of them should be conscious decisions. In my case: I keep the Gmail button and the Steam card because they are part of my profile's identity, but this tutorial also exists to document that I know exactly what I am exposing.

## View counter and sponsor button

Two short badges people ask for the loudest. The most-used view counter is komarev's, and it belongs right under your greeting:

```markdown
![Profile Views](https://komarev.com/ghpvc/?username=Jesus-Valverde&color=blueviolet&style=for-the-badge&label=PROFILE+VIEWS)
```

With the caveats you already know from this ecosystem: the number is approximate (camo's cache filters part of the traffic) and its own maintainer describes it as a "tracking pixel". Avoid the old `visitor-badge.laobi.icu` still circulating in card collections: it is the fragile service of its category. The sponsor button is a badge linking to `github.com/sponsors/YOUR-USERNAME`, with its official logo:

```markdown
[![Sponsor Me](https://img.shields.io/badge/Sponsor_Me-blueviolet?style=for-the-badge&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/Jesus-Valverde)
```

The overlooked detail: the link only works if you have GitHub Sponsors enabled, which is a separate step at github.com/sponsors (available in Mexico; it asks for a Stripe or PayPal account to receive money). You can check whether it is enabled by querying `sponsorsListing` on the GraphQL API for your user. If you would rather skip that signup, Buy Me a Coffee is the no-paperwork alternative, and its badge embeds the same way.

## Generators: the shortcut and its fine print

If you want to skip the manual assembly, two form-based generators do the same job. The biggest by stars is rahuldkjain's (24,500★): you fill in a form (name, tagline, socials, skills) and it generates the Markdown with today's must-have add-ons already wired in — view counter, stats and streak cards, blog posts via Actions, WakaTime, even a Buy Me a Coffee button — with a live preview. The other is GPRM (gprm.itsvg.in): tick boxes per section, a 300+ technology stack picker, and themes. Here this tutorial corrects its own first version: blogs cite GPRM as "the generator" out of inertia, but the data says otherwise — rahuldkjain beats it 24 to 1 on stars. And a fun fact that does circulate wrongly: the blogosphere's most repeated misattribution gives GPRM to JayantGoel001; the actual author is Vishwa Gaurav, verifiable in the repo and its contributors. JayantGoel001 maintains famous template collections, hence the confusion.

For inspiration there are two complementary collections. The canonical gallery of real profiles is `awesome-github-profile-readme` (over 31,000 stars, active as of September 2026): you browse rendered profiles and copy the raw Markdown of the one you like. If you prefer going straight to the source, `Awesome-Profile-README-templates` (11,200★) is an archive of pure templates organized by style — short, elaborate, code-heavy, multimedia — that you open and adapt. And as a card catalog by category there is Profile-Readme-Cards: useful to see the menu at a glance, but verify the freshness of each recommendation — its suggested counter (`visitor-badge.laobi.icu`) is precisely the fragile service in its category. As a healthy ceiling, its own guide says it: one or two cards, three at most.

The shortcut's price: generators produce clone profiles. When thousands of people tick the same boxes, profiles start resembling each other, and feedback threads point it out often. A generator is a good starting point; the value is in what you add afterwards. As for the AI generators that proliferated in 2025-2026: they exist, but nearly all the evidence of their quality comes from the marketing of the people selling them.

## The uncomfortable question: does this get you hired?

We wrote this tutorial under the rule of actively searching for the source that contradicts the premise. The premise was "a decorated profile README helps you professionally". The search's result: there is no quantitative evidence in either direction. No study measures the effect of README decoration on hiring.

What does exist are practitioner anecdotes, and they should be cited as such. The most-cited argument against comes from Underdog.io's blog, a recruiting marketplace (that is, an actor with its own stake in the thesis): recruiters rarely scrutinize GitHub; the useful signal is the code, not the widgets. A Glassdoor thread from July 2025 sums it up with nuance: it does not help with recruiters at all, but it does help with technical hiring managers, who are a minority of the people looking at your profile. And a GitHub community discussion from December 2025 agrees: non-technical reviewers do not read code, though they may glance at activity and polish.

The honest frame I take from all this: a decorated README is cheap garnish, not a strategy. It costs an afternoon, promises nothing measurable, and to the technical minority that does open your profile it communicates care for detail. What actually weighs on your portfolio lives outside the README: pinned repos with real, well-documented code. Decorate on top of that first.

## Checklist: when something does not show up

When your README does not render or something looks broken, check in this order (each step resolves a documented cause):

1. **The profile is blank:** verify the repo is public, the name matches your username exactly, and `README.md` is not empty. The subtle variant: the name is right but the file ended up in a subfolder.
2. **An image looks broken:** open its URL in a private tab. If it returns a 404 or an error page, the URL is malformed. The camo proxy only serves what the origin returns; blaming camo for a broken URL is the classic mistake.
3. **A badge is frozen:** check your repo's Actions tab before blaming the service. If the workflow was auto-disabled by the 60-day inactivity rule, re-enable it and make a commit.
4. **It looks bad on mobile:** GitHub reflows content correctly; the real culprit is usually a fixed-width `<img width="850">`, or a badge wall pushing what matters below the first screen. Put the essentials up top.
5. **A screen reader understands nothing:** every image needs a descriptive `alt`. It is free and it is the first thing a visitor with assistive technology hits.

There is no documented length limit for a README; "keep it short and above the fold" is practitioner consensus, not a GitHub rule.

## Your starter template

With all of the above, here is a minimal, decent base to start yours. Replace the data, commit it to your special repo, and add pieces one at a time:

```markdown
# Hi! I'm YOUR NAME 👋

Student/developer from Mexico 🇲🇽, building things for the web.

- 🔭 Right now: [current project]
- 🌱 Learning: [current technology]
- 📫 Contact: [LinkedIn or form]

## Technologies

[![My Skills](https://skillicons.dev/icons?i=js,html,css,react&theme=dark)](https://skillicons.dev)

## Stats

![My GitHub stats](https://github-readme-stats.vercel.app/api?username=YOUR-USERNAME&show_icons=true&theme=tokyonight)

<details>
<summary>More about me</summary>

Whatever you want to tell, with a blank line before it so it renders.

</details>
```

Every piece you add afterwards (streak, snake, counter) — you already know what it costs, who it depends on, and how to fix it when it breaks. That knowledge is the difference between a profile that looks good on tutorial day and one that is still alive a year later.

---

## Key takeaways

If you forget everything else, let this survive:

1. The whole mechanism is three conditions: a public repo named exactly after your username and a non-empty `README.md` at its root.
2. Data cards are images served by third parties; the robust way is self-hosting the stats instance and preferring "committed" widgets that save the SVG to your own repo.
3. "My card is stale" almost always means two stacked caches: the widget's and camo's; the cheap fix is `&v=2`.
4. Scheduled workflows auto-disable after 60 days without repo activity; your snake freezes silently.
5. Tokens go with minimum scope, in secrets, never in plain text; and the professional benefit of a decorated README is anecdote, not data: pinned repos with real code come first.

## Reflection questions

- If `card.yuy1n.io` (or any service you use) shut down tomorrow, which blocks of your profile would die and which would survive? Do the inventory.
- Your profile has an audience that almost never arrives (recruiters) and one that does arrive and reads code (hiring managers, other devs). Is your README designed for the audience that actually opens your profile?
- What does your README expose today that is not a conscious decision of yours?

## Glossary

- **PAT (Personal Access Token):** a personal access key that authorizes programs and Actions to act on your GitHub account with the permissions (scopes) you assign them.
- **Camo:** GitHub's proxy that rewrites every external image in a README to `camo.githubusercontent.com`; it protects visitor privacy and caches images.
- **Rate limit:** the number of requests an API allows in a period; when it runs out, the API responds with an error.
- **Self-hosting:** deploying your own copy of a service (for example, github-readme-stats on your Vercel account) so you do not depend on the shared instance.
- **Commit:** saving a change to a Git repository's history.
- **Cron:** a task scheduler; in GitHub Actions it defines how often a workflow runs (for example, daily at midnight UTC).
- **SVG:** a vector image format that GitHub renders in READMEs; it is the native format of almost every widget.
- **Scope:** the level of permission granted to a token; the principle is to assign the minimum needed.

## Main sources

- GitHub Docs — Managing your profile README; Basic writing and formatting syntax; About anonymized URLs; Disabling and enabling a workflow (verified 2026-10-27)
- Raw README of the `Jesus-Valverde/Jesus-Valverde` profile (2026-10-27)
- anuraghazra/github-readme-stats (README + discussion #4433); DenverCoder1/github-readme-streak-stats; ryo-ma/github-profile-trophy
- Platane/snk (repo and its own workflow); lowlighter/metrics; gautamkrishnar/blog-post-workflow
- tandpfun/skill-icons (issue #1491); syvixor/skills-icons; badges/shields (docs + issue #12162); kyechan99/capsule-render; DenverCoder1/readme-typing-svg
- antonkomarev/github-profile-views-counter (issues #90 and #121); vn7n24fzkq/github-profile-summary-cards; yoshi389111/github-profile-3d-contrib
- VishwaGauravIn/github-profile-readme-maker; abhisheknaiidu/awesome-github-profile-readme
- The Register (Dec 17, 2025) and github.blog changelogs (Jan 2026, Sep 28, 2026) on pricing and runners
- Underdog.io, a Glassdoor thread (Jul 2025), and discussion #182100 (Dec 2025) — anecdotal counter-premise evidence

---
