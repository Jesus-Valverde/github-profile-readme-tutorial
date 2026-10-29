[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md) [![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)

# How to Customize Your GitHub Profile README (with my profile as the example)


This tutorial walks you through building your GitHub profile README: the special repo that activates it, badges, the automatic stats cards, the snake with GitHub Actions, and the mistakes that leave profiles broken. Everything is tested on my own profile, which I use as the example throughout.

## How to create your README and get it shown on your profile

GitHub shows a README on your profile when you meet three conditions:

1. The repository is **public**.
2. The repo name is exactly your username (in my case, `Jesus-Valverde`).
3. The repo has a `README.md` file with content, at its root.

If any of the three is missing, your profile stays blank. There is nothing else to configure.

To create it: on github.com, click `+` → **New repository**. Name it exactly like your username, set it to **Public**, tick **Add a README**, and create the repo. When you open it, GitHub detects that it is your special repo and shows an **Edit README** button right on your profile.

Three special cases:

- If your account is managed by a company through GitHub Enterprise Managed Users, you cannot have a personalized profile; the official documentation excludes it.
- If you created a repo with your name before July 2020, it does not show up automatically: open the repo and press **Share to profile**.
- Achievements still exist as of October 2026, but the documentation has dead pages and two badges can no longer be earned. Treat them as decoration, not as a goal.

## My profile as the example

This tutorial was born from a real pending item: my profile had a section saying "👉 Tutorials", with a "loading..." GIF and the admission that it was unfinished. What follows is the anatomy of what I already built: what it does well, what it was missing, and what is fragile.

My `README.md` weighs 3,369 bytes and has this structure: a greeting, the Tutorials section (the placeholder), a "who am I" section with the Mexican flag, another on my studies, a row of 11 technology badges, 3 buttons to practice platforms (freeCodeCamp, Exercism, HackerRank), 3 contact buttons (LinkedIn, Linktree, email), and a card from my Steam profile. That is 17 badges in total, all served by shields.io with the `for-the-badge` style.

Each badge looks like this (a real one, copied from my file):

```markdown
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
```

Two things my profile gets right without having planned it: every image has alternative text (`alt`) and the sections use proper `##` headings. That makes it readable for screen readers, which is exactly what GitHub's accessibility guidance recommends for profiles.

What it was missing: stats cards, a contribution streak, and the snake. And two fragilities worth pointing out because you can fall into them too: my Steam card is served by a community service (`card.yuy1n.io`) with no backing — if that service shuts down, the largest block of my profile breaks. And the email button uses a `mailto:` link with my Gmail in plain sight, which spam harvesters read with pleasure. The locks come further down.

## Badges with shields.io

A badge is an image that shields.io generates from its own URL. The basic format is `img.shields.io/badge/LABEL-MESSAGE-COLOR`, and most of the control lives in the URL parameters: `style` picks the style (`flat` is the default; also `flat-square`, `plastic`, `for-the-badge`, and `social`), `logo` takes the name of any icon in the simple-icons catalog, and `logoColor` and the badge color accept hex colors.

Three escaping rules cause 90% of broken badges:

- The hyphen `-` separates segments, so a literal hyphen is written `--`.
- A literal underscore is written `__`.
- The `#` of hex colors is encoded as `%23` (a bare hex without `#` also works).

To make a badge clickable, do not use the `link=` parameter (it does not work inside `<img>`): wrap the Markdown image in a normal link:

```markdown
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/your-username/)
```

On limits: shields.io publishes no quota figures; real bottlenecks usually sit in the external service the badge queries, not in shields itself.

## Icons without text with skill-icons

A compact alternative to badge rows is skill-icons: a single URL that draws a grid of rounded icons.

```markdown
[![My Skills](https://skillicons.dev/icons?i=js,html,css,react,py,flask&theme=dark)](https://skillicons.dev)
```

Ids are lowercase names (`js`, `py`, `react`, `nextjs`, `kubernetes`...), the default theme is `dark`, and `perline` controls how many icons go per line (1 to 50). The downside: with no text next to them, a wall of logos is less legible to whoever does not recognize the icons. For a portfolio, named badges communicate better; compact icons win when the list is long.

If an icon you need is missing: skillicons.dev does not have them all (React Router and JWT return empty squares). The alternative `skills.syvixor.com` has over 1,059 icons — including `reactrouter` and `jwt` — and switches between light and dark theme based on the visitor's preference.

## A README in two languages

To offer your profile in more than one language, put a row of language badges at the top of the README, each linking to its version:

```markdown
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](README.es.md)
```

The file convention is a language suffix: `README.md` as the primary and `README.es.md` for Spanish. Every version carries the same badge row, so readers can hop between languages from any of them. Keep in mind that GitHub only renders `README.md` on your profile page (it does not run JavaScript, so there is no "on-site" language switcher): the badge leads to the repo, where the full other-language version does render.

## GitHub's native formatting

Before installing anything, use what GitHub already supports: collapsible sections, callouts, footnotes, and a tag for images that follow the visitor's light/dark theme. No external services, no tokens, no maintenance.

Collapsible section (useful so you do not flatten your visitor with text):

```html
<details>
<summary>My journey in detail</summary>

Content goes here. There must be a blank line after `<summary>`
for the inner Markdown to render.

</details>
```

The callouts (`[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, `[!CAUTION]`) are written inside a blockquote. The official documentation asks for moderation: at most one or two per document, only for crucial information. Note: they render on github.com only; on other viewers they degrade to a plain blockquote.

And the most underrated native feature: the image that changes with the visitor's theme.

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="banner-dark.svg">
  <img alt="Welcome banner" src="banner-light.svg">
</picture>
```

## Banners and animated effects (in moderation)

If you want a header with presence, the two standard tools are capsule-render (animated SVG banners) and readme-typing-svg (text that types and deletes itself).

```markdown
![header](https://capsule-render.vercel.app/api?type=wave&color=gradient&height=200&section=header&text=Your%20Name&fontSize=42&animation=fadeIn)

![typing](https://readme-typing-svg.demolab.com/?font=Fira+Code&size=22&pause=1000&multiline=true&width=600&height=80&lines=Web+developer;Learning+Flask+and+React)
```

The `multiline=true` parameter stacks several phrases separated by semicolons, instead of retyping everything on one line.

Before filling your profile with effects, consider the cost: each effect is one more external dependency, decorative GIFs weigh megabytes, none respects the system's reduced-motion preference, and an animated banner + animated text + GIF + badges together give you the saturated profile the community points to as a bad example. My rule, drawn from my own profile: the "loading..." GIF works because there is exactly one and it tells a story. Two more would be noise.

## Stats cards

Here lives the heart of the ecosystem: community services that turn your GitHub activity into image cards.

The statistics card, by anuraghazra (github-readme-stats):

```markdown
![My GitHub stats](https://github-readme-stats.vercel.app/api?username=Jesus-Valverde&show_icons=true&theme=tokyonight)
```

The contribution streak card, by DenverCoder1:

```markdown
![GitHub Streak](https://streak-stats.demolab.com?user=Jesus-Valverde&theme=tokyonight)
```

The trophy card, by ryo-ma:

```markdown
![Trophy](https://github-profile-trophy.vercel.app/?username=Jesus-Valverde)
```

And a fourth one people often forget, the only truly automatic one: the most-used languages card. GitHub computes it from your actual repos — the badge row counts what you claim to know; this one counts what your code says you do:

```markdown
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Jesus-Valverde&layout=compact&theme=tokyonight&langs_count=8)
```

Useful parameters on the stats card: `include_all_commits=true` counts lifetime commits (without it, the current year only), `hide_border=true` blends it into the background, `layout=compact` turns the languages card into a compact list instead of bars, `langs_count` controls how many languages it shows, and `cache_seconds` controls how long the image is cached (6 hours minimum, 24 maximum).

If you place two cards side by side (with percentage `width`, so they stack on mobile), anchor them with `align="top"`: GitHub aligns images by their text line, and since the cards have different natural heights, the shorter one floats downward. If you also want them to measure the same, compensate with the width split: my stats card measures 467×195 pixels and the streak card 495×195; with `width="48%"` and `width="51%"` they stay matched at any window size.

The problem to know about before installing anything: hosted instances share GitHub's anonymous API quota and therefore fail intermittently. The fix recommended by the project's own team is deploying your instance on Vercel, and it takes about 15 minutes: fork the repo, connect it to Vercel, and in Vercel's environment variables add `PAT_1` with a classic Personal Access Token (PAT: the key GitHub uses to authorize programs) with no permissions checked. Then change the card URL from `github-readme-stats.vercel.app` to your instance's. The streak card documents the same process; the trophy service is still up as is.

## Other widgets

A second circle of popular widgets exists. What decides their robustness is who serves the image when someone visits your profile:

| Widget | Who serves the image? | If the third party fails |
|---|---|---|
| Views counter (komarev) | Their server, on every visit | Broken or stale badge |
| Activity graph (ashutosh00710) | Their Vercel, on every visit | Broken image (same risk as stats) |
| Summary cards (vn7n24fzkq) | An Action **saves the SVGs to your repo** | Nothing: the image is yours |
| 3D contributions (yoshi389111) | An Action saves the SVG to your repo | Nothing: same pattern |
| WakaTime (coding time) | Their API + a daily Action | Empty section or error |

The most robust pattern in the ecosystem is "committed": the Action runs in your repo, generates the SVG, and saves it as part of your repository. The image the visitor loads lives on `raw.githubusercontent.com` — on GitHub, not on somebody else's server that can fail at 3 a.m.

Two warnings from this circle: the views counter is approximate (GitHub's cache filters part of the traffic; its own maintainer describes it as a "tracking pixel", and it has stopped displaying under load), and WakaTime requires enabling "Display activity publicly" on your WakaTime account and updates once a day.

## The snake with GitHub Actions

The ecosystem's most beloved animation is the snake eating your contribution grid (Platane/snk). Here the image is generated inside your own repo and saved to a branch named `output` — after that, it depends on nobody.

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

On public repos workflows are free, and a daily snake run takes about a minute. The mistake that breaks more profiles than you would imagine: **if your repo goes 60 days without activity, GitHub disables scheduled workflows automatically.** There is no warning on the README — your snake simply stays frozen on the last SVG, and it looks like the service's fault when the workflow is just paused. The fix: Actions tab → select the workflow → Enable workflow, and make a commit to reset the clock.

One more maintenance note: use recent versions of actions. Their runtime migrates every year (from Node 20 to Node 24 as of June 2026), and old actions stopped running.

Two more automations if you need them: lowlighter/metrics generates infographics with 30+ plugins (its shared instance is chronically rate-limited; the stable path is running it as an Action in your repo), and gautamkrishnar/blog-post-workflow inserts your recent posts between two comment tags, via RSS.

## Why your card shows stale data

You updated your stats and the card still shows yesterday's data. Almost always it is caching, and there are two layers:

1. **The widget's cache:** github-readme-stats' `cache_seconds` keeps the image for 6 hours by default.
2. **camo's cache:** every external image in a README goes through GitHub's proxy (`camo.githubusercontent.com`), which keeps its own copy.

The quick fix is making camo see a new URL: append a throwaway parameter (`&v=2`, then `&v=3`...). There is also a `curl -X PURGE` against the camo URL to invalidate one specific image, but use it sparingly: it forces every GitHub user to re-download the image.

A privacy bonus: since the one requesting the external service is GitHub's proxy and not the visitor's browser, widgets do not see your readers' IPs.

## Security: tokens and what you expose

Three non-negotiable rules:

1. **Every tool gets the minimum token.** The self-hosted stats instance uses a classic PAT with no permissions (in Vercel environment variables, not repo secrets); Actions that save files to your repo (snake, summary cards, 3D) use a fine-grained token limited to that repo; metrics uses a no-permission PAT for public data.
2. **A token never goes in the README, in the workflow YAML, or in a commit message.** GitHub's secret protection detects the `ghp_` and `github_pat_` patterns on push, but do not rely on that alone.
3. **If a token leaks, revoke it immediately** under Settings → Developer settings. Deleting the commit revokes nothing.

And the part almost nobody reviews before publishing: what your README says about you to people who are not your audience. A `mailto:` with your email in plain sight guarantees spam (JavaScript or image obfuscation does not work: harvesters defeat it). A public Steam card exposes your library, your playtime, and your friends list. View counters collect telemetry from your profile. None of these is wrong by definition; all of them should be conscious decisions. In my case I keep the Gmail button and the Steam card because they are part of my profile's identity — and I know exactly what I am exposing.

## View counter and sponsor button

Two short badges almost everyone asks for. The most-used view counter is komarev's, and it belongs right above the greeting:

```markdown
![Profile Views](https://komarev.com/ghpvc/?username=Jesus-Valverde&color=blueviolet&style=for-the-badge&label=PROFILE+VIEWS)
```

Remember the number is approximate (the cache filters part of the traffic). Avoid `visitor-badge.laobi.icu`, still circulating in card collections: it is the most fragile service in its category.

The sponsor button is a badge linking to your GitHub Sponsors page:

```markdown
[![Sponsor Me](https://img.shields.io/badge/Sponsor_Me-blueviolet?style=for-the-badge&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/Jesus-Valverde)
```

The overlooked detail: the link only works if you have GitHub Sponsors enabled, which is a separate step at github.com/sponsors (available in Mexico; it asks for a Stripe or PayPal account to receive money). If you would rather skip that signup, Buy Me a Coffee is the no-paperwork alternative, and its badge embeds the same way.

## Automatic generators

If you want to skip the manual assembly, there are two form-based generators: rahuldkjain's (at `rahuldkjain.github.io/github-profile-readme-generator`; you fill in name, tagline, socials and skills, and it generates the Markdown with a live preview) and GPRM (`gprm.itsvg.in`; tick boxes per section, 300+ technologies, themes).

For inspiration, two complementary collections: `awesome-github-profile-readme` (over 31,000 stars; browse rendered real profiles and copy the Markdown of the one you like) and `Awesome-Profile-README-templates` (11,200★; pure templates organized by style — short, elaborate, code-heavy, multimedia). As a healthy ceiling, the guide itself says it: one or two cards, three at most.

The shortcut's cost: generators produce clone profiles. When thousands of people tick the same boxes, profiles start resembling each other. A generator is a good starting point; the value is in what you add afterwards. As for the AI generators that proliferated in 2025-2026: they exist, but nearly all the evidence of their quality comes from the marketing of the people selling them.

## Does a decorated README help you get hired?

I deliberately searched for evidence against the premise "a decorated profile README helps you professionally", and the result is: no study measures it in either direction.

What exists are practitioner anecdotes, cited as such: recruiters rarely scrutinize GitHub (the useful signal is the code, not the widgets); technical hiring managers do open the profile and value the polish, but they are a minority of the people who look at it. The practical conclusion: a decorated README is cheap garnish that communicates care to whoever reads code — it costs an afternoon and promises nothing measurable. What actually weighs on your portfolio lives outside the README: pinned repos with real, well-documented code. That base first; decoration on top.

## Troubleshooting

When your README does not render or something looks broken, check in this order:

1. **The profile is blank:** verify the repo is public, the name matches your username exactly, and `README.md` is not empty or in a subfolder.
2. **An image looks broken:** open its URL in a private tab. If it returns a 404 or an error page, the URL is malformed (check the badge escaping rules).
3. **A badge is frozen:** check your repo's Actions tab before blaming the service. If the workflow was auto-disabled by the 60-day inactivity rule, re-enable it and make a commit.
4. **It looks bad on mobile:** the culprit is usually a fixed-width image (`<img width="850">`) or a badge wall pushing what matters below the first screen. Put the essentials up top.
5. **A screen reader understands nothing:** every image needs a descriptive `alt`. It is free and it is the first thing a visitor with assistive technology hits.

There is no documented length limit for a README; "keep it short and the important part up top" is practitioner consensus, not a GitHub rule.

## Starter template

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

## The essentials in 5 points

1. The whole mechanism is three conditions: a public repo, a name exactly matching your username, and a `README.md` with content at its root.
2. Data cards are images served by third parties; the robust way is self-hosting the stats instance and preferring widgets that save the SVG to your own repo.
3. "My card is stale" almost always means two stacked caches: the widget's (6 h) and camo's; the cheap fix is `&v=2`.
4. Scheduled workflows auto-disable after 60 days without repo activity; your snake freezes silently.
5. Tokens go with minimum permissions, in secrets, never in plain text; and the professional benefit of a decorated README is anecdote, not data: pinned repos with real code come first.

## Sources

- GitHub Docs — Managing your profile README; Basic writing and formatting syntax; About anonymized URLs; Disabling and enabling a workflow (verified 2026-10-27)
- Raw README of the `Jesus-Valverde/Jesus-Valverde` profile (2026-10-27)
- anuraghazra/github-readme-stats (README + discussion #4433); DenverCoder1/github-readme-streak-stats; ryo-ma/github-profile-trophy
- Platane/snk (repo and its own workflow); lowlighter/metrics; gautamkrishnar/blog-post-workflow
- tandpfun/skill-icons; syvixor/skills-icons; badges/shields (docs); kyechan99/capsule-render; DenverCoder1/readme-typing-svg
- antonkomarev/github-profile-views-counter; vn7n24fzkq/github-profile-summary-cards; yoshi389111/github-profile-3d-contrib
- VishwaGauravIn/github-profile-readme-maker; abhisheknaiidu/awesome-github-profile-readme
- The Register (Dec 17, 2025) and github.blog changelogs on pricing and runners
- Underdog.io, a Glassdoor thread (Jul 2025), and discussion #182100 (Dec 2025) — anecdotal counter-premise evidence
