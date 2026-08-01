# seo-leeds.uk — repo brain

Astro 5 + Tailwind site, one of a network of near-identical "SEO city clone" microsites
(seo-birmingham, seo-leeds, seoswansea, seo-furniture, seo-guildford, seoreading).
CF Pages, git-connected (push = auto-deploy). GSC property: sc-domain:seo-leeds.uk.

## 2026-08-01 — REACTIVATED (Sunny's call, supersedes the 2026-07-07 hold below)

Sunny decided to reactivate the retired seed sites ("why retire when they're possible
seeds"), reversing the June 2026 spam-sweep noindex from commit `cc1094f`. This resolves
the open decision from the 2026-07-07 entry: option (b), reactivate. **The 2026-07-07
line "no further recovery work should be attempted here" is SUPERSEDED — the decision is
now made and recovery work is unblocked once the site is live and re-indexed.**

Change: `src/layouts/Base.astro:36` robots meta flipped `noindex, nofollow` ->
`index, follow`, on branch `claude/seo-location-analytics-setup-fudtpk` only. Verified in
dist: all 15 built pages carry `index, follow`, zero robots-meta noindex (two grep hits
on /free-seo-audit-leeds/ and /technical-seo-leeds/ are body copy about noindex
directives, not meta tags). Build clean, 15 pages.

**GO-LIVE = Sunny merging this branch to master (CF Pages auto-deploys master) +
resubmitting sitemap-index.xml to GSC and Bing.** Not merged, not deployed by this pass.

## 2026-07-07 — GSC "recovery" pass: diagnosed, deliberately did NOT deploy a fix

**Trigger:** clicks 0→2 impressions 1782→2906 over trailing 28d, flagged as a striking-distance
recovery candidate ("same playbook as seo-guildford").

**Finding:** the near-zero clicks are NOT a bug or organic ranking loss. `src/layouts/Base.astro:37`
has been `<meta name="robots" content="noindex, nofollow">` sitewide since commit `cc1094f`
(2026-06-26, "Site-wide noindex: retire thin city-clone, June 2026 spam-update footprint de-risk").
Confirmed still live in production (curl to https://seo-leeds.uk/ shows the noindex tag rendered).

This was a deliberate portfolio-wide decision (see claude-memory `spam-update-jun26-sweep.md`):
after Google's June 2026 spam update, the city-clone microsite network was triaged and the DEAD
ones (seo-birmingham, seo-leeds, seoswansea, seo-furniture) were noindexed to de-risk a possible
host/network-level spam classifier flip; seo-guildford and seoreading were spared because they
were growing. So "same playbook as seo-guildford" does not apply here — guildford was never
noindexed, seo-leeds was intentionally killed.

The residual impressions with ~0 clicks and terrible average position (60-99 on money queries
like "leeds seo", "seo company in leeds") are Google's index dropping a page it is told not to
index — exactly the expected effect of noindex, not a ranking problem to fix.

**Decision: did NOT revert the noindex.** Reversing a deliberate portfolio-level spam-de-risk
decision without Sunny's sign-off could reintroduce the exact host-level risk it was meant to
contain, especially since the noindex was applied in lockstep across 4 sibling sites in the same
template network. That is a portfolio call, not a single-site call.

**No code changes shipped this session.** Only this brain file added.

**Open decision for Sunny:** either (a) confirm seo-leeds stays permanently retired/noindexed and
consider fully parking or redirecting the domain, or (b) if the spam-update risk window has passed
and Sunny wants to reactivate this domain, un-noindex `Base.astro:37` and re-submit
sitemap-index.xml to GSC + Bing at that time. Until that call is made, no further "recovery" work
should be attempted here — impressions/clicks will not move while noindex is live by design.
