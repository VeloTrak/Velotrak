# VeloTrak compared with other ad trackers

This page compares VeloTrak with Voluum, RedTrack, Binom, BeMob, Keitaro, and FunnelFlux on facts that were on each vendor's own site on **13 Nov 2026**. It is not a feature-complete matrix, and it does not treat one vendor's "event" as equal to another's.

VeloTrak facts are from https://velotrak.app/ and https://velotrak.app/llms.txt. Competitor facts are from the pages linked in each section. Prices change, and two of the pages were running a promotion that day.

## Side by side

| | VeloTrak | Voluum | RedTrack | BeMob | FunnelFlux Pro | Keitaro | Binom |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Hosting | Your Linux server | Vendor cloud (SaaS) | Vendor cloud | Vendor cloud | Vendor cloud | You install it; you buy the server | Self-hosted, or their cloud plan |
| Click storage | Your ClickHouse; ledger in your PostgreSQL | Their cloud | Their cloud | Their cloud | Their cloud | The server you run | Your server, or their cloud |
| Fee vs. volume | Flat. Clicks are not metered on any plan. | Included events, then overage | Included events, then overage | Included events, then overage on paid plans | Included events, then overage | License by edition. No event quota on the public price list. | Flat license. Their FAQ says you are not billed per click. |
| Entry published price | Free. Pro $49/month or $490/year. | Profit shown at $119/month in the compare table | Solo $169/month, or $118/month on the annual price shown that day | Free to 100,000 events. Professional $49/month for 1,000,000 events. | $99/month includes 2 million events | Yearly toggle: Starter €40/month | v2 price page shows $149 and $104 |
| AI access (MCP) | 90 tools. Read-only on Free. Diff, then confirm, on edits and deletes. | Listed, with a daily request cap by plan | Listed on Solo ("MCP and API access") | Not stated on the pricing page we checked | Not stated on the pricing page we checked | Documented. Expert, Team, and Enterprise, from version 11.5.0. | Not stated on the price page we checked |
| CAPI | Meta, TikTok, and Google on every plan, including Free | Not verified from the pricing-page text fetched this day | Pricing page: Conversion API on every affiliate/lead-gen plan | Not verified from the pricing page | Help center describes S2S and pixels; a CAPI matrix was not on the pricing block | Pricing API lists Facebook on Advanced and above, and Google Ads plus TikTok on Expert and above. Docs also cover FB Pixel and TikTok Pixel. | Not stated on the price page we checked |

VeloTrak's license never includes the VPS. Budget both. The site says a VPS from about $10/month runs the 2 vCPU / 4 GB floor.

## What "events" means

Do not compare a 10-million figure across these products without reading the definition.

- **VeloTrak.** Clicks are not metered. Plan limits are things like active campaigns, report history, dimensions, CAPI accounts, and seats — not a click quota.
- **Voluum.** Docs: paid events are visits, clicks, and conversions. The pricing page also says the quota counts visits, clicks, conversions, and impressions, and that 10 impressions count as 1 event. Past the quota, tracking continues and overage is billed. Their FAQ gives the Profit example: $0.06 per 1,000 events past 1,000,000.
- **RedTrack.** Pricing copy: tracked events are clicks, conversions, and postbacks per month. Overage is per 1,000 events above the allowance.
- **BeMob.** Pricing footnote: an event is every impression, visit, click, or conversion. The free plan cannot pay overage. Paid plans can.
- **FunnelFlux Pro.** Billing notes: events include visits, clicks, condition and rotator node visits, conversions, and custom events. Extra events past the included 2 million are $10 per million. Their help center also describes overage as $0.01 per 1,000 events.
- **Keitaro.** The public individual price list we checked is organized by users, domains, and integrations, not by an event cap.
- **Binom.** The price page says one price for any click volume, and the FAQ says a large number of clicks is still the license fee only. The v2 card also says "Traffic up to 260m/day", so "not billed per click" and "a stated throughput ceiling" are both on that page.

## VeloTrak

Source: https://velotrak.app/ and https://velotrak.app/llms.txt

- Self-hosted. One Go binary, PostgreSQL, ClickHouse. Install: `curl -fsSL https://velotrak.app/install.sh | sudo bash`
- Free $0. Pro $49/month or $490/year (shown as $41/month on the annual toggle). Team $99/month or $990/year (shown as $83/month on the annual toggle). Founder $399 once.
- CAPI for Meta, TikTok, and Google on every plan.
- MCP: 90 tools. Edits and deletes require a diff and a confirmation. Free is read-only.
- Full export. Telemetry off by default. 30-day offline grace if licensing fails.

## Voluum

Sources: https://voluum.com/pricing/ and https://doc.voluum.com/article/tracking (fetched 13 Nov 2026). The pricing page was showing a "Black Month" promotion.

- Cloud SaaS. Their pricing FAQ says infrastructure is on them.
- Plan cards list event caps including Profit up to 1,000,000, Scale up to 5,000,000, and Start-up up to 10,000,000.
- The compare table on that page opened with **Profit at $119/month**. Further columns listed more event quotas (5M, 10M, 10M, 25M, 60M) and more monthly prices. Those higher prices were not clearly tied to plan names in the text of the page, so they are not assigned to tiers here. Read the live table before you buy.
- Overage on the compare table runs from $0.06 to $0.03 per 1,000 events. The FAQ explicitly uses $0.06 per 1,000 for Profit past 1,000,000 events.
- Voluum MCP is listed on the plan cards with a daily cap: 20 requests/day on Profit, 60 on Scale, 100 on Start-up, and higher caps on higher cards. The page says the scope can be increased as an add-on.

## RedTrack

Source: https://www.redtrack.io/pricing/ (fetched 13 Nov 2026). The page said "Black Friday: 30% off the 12-month price" and that the renewal keeps that price. https://www.redtrack.io/ describes the product as cloud-hosted, with no servers to run.

Affiliate / lead-gen plans on that page:

| Plan | Events / month | Price shown |
| --- | --- | --- |
| Solo | 5 million, 1 user | $118/month and $169/month; $1,420 billed yearly |
| Team | 20 million, 5 users | $279/month and $399/month |
| Enterprise | 75 million, 15 users | $699/month and $999/month |

The lower monthly figure is the annual-billing price; the higher one is monthly billing. Solo's feature list includes sending conversions back with CAPI, and "MCP and API access". There is a 14-day trial. A separate ecommerce price list (Relay, Brand, Agency) is on the same page and is not the affiliate plan table above.

Their help center says there is no free plan: https://help.redtrack.io/ufaq/is-there-a-free-plan-available/

## BeMob

Sources: https://bemob.com/pricing/ and https://bemob.com/ (fetched 13 Nov 2026). The homepage describes tracking on BeMob's auto-scaling servers rather than a server you install.

| Plan | Events / month | Data retention | Price |
| --- | --- | --- | --- |
| Free | 100,000 | 1 month | $0. Overage cannot be purchased. |
| Professional | 1,000,000 | 1 month | $49/month. Overage $0.05 per 1,000 events. |
| Business | 10,000,000 | 3 months | $249/month. Overage $0.025 per 1,000. |
| Enterprise | 30,000,000 | 6 months | $499/month. Overage $0.02 per 1,000. |

An event, in their footnote, is every impression, visit, click, or conversion.

## FunnelFlux

There are two products, and the vendor's own help page says they are not the same thing: https://help.funnelflux.pro/en/article/funnelflux-pro-vs-funnelflux-original-1hq5lah/

- **FunnelFlux Pro** is the current cloud product. On https://funnelflux.com/pro (13 Nov 2026) the billing notes say the base plan is **$99/month and includes 2 million events**, then **$10 per extra million**. A 14-day trial requires a payment method. The first two custom domains are free; more are $2 each per month. A standby plan is listed at $9/month to keep data after a subscription ends.
- **FunnelFlux original** is the older self-hosted product with a flat license. The same help page says it is still maintained and is no longer the focus, and that Pro bills by visitors / events instead. This page does not quote an original-license price because no current price was on the Pro page we fetched.

Event definition and the $0.01-per-1,000 overage wording: https://help.funnelflux.pro/en/article/what-counts-as-an-event-m2s3ah/

## Keitaro

Sources: https://keitaro.io/en/pricing and the pricing API `https://keitaro.io/pricing_api/v4/pricing/9` (fetched 13 Nov 2026). Install docs start at https://docs.keitaro.io/en/get-started/auto-installation.html. MCP docs: https://docs.keitaro.io/en/settings/mcp.html

The yearly individual toggle displayed:

| Edition | Price on the yearly toggle | Limits in the pricing API |
| --- | --- | --- |
| Starter | €40/month | 1 user, 1 domain |
| Advanced | €72/month | 1 user, 100 domains; Facebook integration |
| Expert | €104/month | 5 users, 500 domains; Facebook, Google Ads (5), TikTok (5) |

The API also lists a 20% discount on a 12-month term (`"discounts":{"1":0,"12":20,"6":10}`) and higher business editions (Team and Enterprise) with higher list prices. Currency on the HTML pricing page is euros. Keitaro's own docs start with an installation guide, and the pricing page asks "Do I need to purchase hosting?" — the license is not a hosted login. The answer text under that question was not in the static HTML.

MCP, from their docs: available on Expert, Team, and Enterprise from Keitaro 11.5.0 (stable) or 11.5-beta. Default mode is read-only. Edit mode can create and change campaigns, streams, and offers. The docs tell you to check an edit before confirming, because the model can misunderstand a request. Landing pages are a read-only list. Tracker settings, users, bot lists, and cost updates are not MCP tools.

## Binom

Sources: https://binom.org/price and https://binom.org/changelog (fetched 13 Nov 2026).

- The v2 price card shows **$149** and **$104** under the monthly and yearly toggles, and an additional license at $75 and $52 in the same pattern. Treat $104 as the yearly figure only after you confirm the toggle, which is how that pair is laid out.
- The page headline is "One price for any clicks volume." The FAQ says traffic is not billed on top of the license, and that you can cancel.
- The same v2 card lists "Traffic up to 260m/day", unlimited users, unlimited domains, and a 30-day trial.
- **Binom Cloud** is listed at $299, with traffic up to 2 million a day. Their FAQ says cloud plans came later and include the server.
- Their changelog's 2.28.00 entry (02.12.25) says the tracker runs on **PHP 8.4**. Older install docs that still mention PHP 7.4 are not the current changelog.

Binom's price page does not describe an MCP server or a native conversions API. Absence on that page is not a proof that the feature is missing; check Binom's current docs if you need that row.

## What this page does not claim

- It does not claim a dollar saving at a given volume. VeloTrak's homepage has a calculator; the inputs are the other vendors' published tiers, and those tiers were on promotion or were easy to mis-assign on 13 Nov 2026. Use the links above and your own event definition.
- It does not rank redirect speed. VeloTrak's published 3,071 clicks/second figure is a single-box load test described in [the FAQ](faq.md). Other vendors publish their own numbers under their own methods.
- It does not treat "has MCP" as the same capability. VeloTrak documents 90 tools and a diff-then-confirm step. Voluum documents a daily request cap. Keitaro documents edition gates and an edit mode. RedTrack lists MCP access on Solo. Those are different designs.
