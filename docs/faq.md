# VeloTrak FAQ

Answers below are the product facts published on https://velotrak.app/, https://velotrak.app/llms.txt, the privacy policy, and the terms of service, checked 13 Nov 2026. Install details that come from the v1.0.0 binary are marked as such.

## What is VeloTrak?

VeloTrak is a self-hosted ad tracker. Clicks and conversions stay in PostgreSQL and ClickHouse on your server. The license is a flat price, not a per-click fee. CAPI for Meta, TikTok, and Google is on every plan, and 90 MCP tools are available to an AI assistant.

VeloTrak the ad tracker is not the Timex Velo-Trak cycling watch.

## Is self-hosting a hassle? What server do I need?

One install command sets up VeloTrak with PostgreSQL and ClickHouse:

```bash
curl -fsSL https://velotrak.app/install.sh | sudo bash
```

Minimum: 2 vCPU / 4 GB, sized for at least 800 clicks per second (about 69 million a day). Recommended: 4 vCPU / 8 GB. A VPS from about $10/month runs the floor tier. The five-step wizard does not require editing a config file. Linux x86_64 or arm64 with systemd is required. See [installation.md](installation.md).

## If my server loses internet, or licensing breaks, does tracking stop?

No. Licensing is separate from the click path. There is a 30-day offline grace period. A licensing problem does not stop tracking.

## What does the free plan include, and where does it stop?

Clicks are never metered on any plan. Free runs up to 3 active campaigns, 1 user, and 1 install. Reports cover the last 15 days and 2 dimensions; older data is kept. CAPI is included on all three platforms with 1 account each. You can import up to 20 campaigns at a time (campaigns past the 3 active ones land paused, so the import does not drop them). MCP is read-only. Email alerts are included. When you hit a limit, the app shows what Pro or Team unlocks.

## What do Pro, Team, and Founder cost?

USD, as shown on https://velotrak.app/#pricing:

- **Pro** — $49/month, or $41/month when billed annually at $490/year. Unlimited campaigns, full report history, 5 dimensions, unlimited CAPI accounts and imports, custom metrics, automatic cost sync, alerts that can pause losing campaigns, MCP read/write (90 tools), scheduled email reports, Telegram and webhook alerts, LP Protect, your branding, up to 3 admin users, 1 install per seat, email support.
- **Team** — $99/month, or $83/month when billed annually at $990/year. Everything in Pro, plus unlimited users with operator or viewer roles, an audit log, API keys, one MCP token per teammate or agent, 3 installs per seat, and priority support.
- **Founder** — $399 once, presale, 100 seats. All Pro features for life on 1 install, with 12 months of updates included.

Annual billing is 12 months for the price of 10. You can cancel anytime; the plan stays usable until the end of the current period. A full refund is available within 14 days of purchase, including Founder. After a refund, that license is revoked.

## I'm on another tracker. How painful is migration?

Free imports up to 20 campaigns at a time. Beyond 3 active campaigns they land paused, so nothing is thrown away. Pro and above import without that limit, with mappings built in.

## Does any of my data reach VeloTrak's servers?

No. Clicks, conversions, campaigns, and the ledger stay in your PostgreSQL and ClickHouse. Telemetry is off by default. Full export is always available.

When a paid license activates and checks in, the licensing service receives an install identifier, the software version, the plan, and the license status. The privacy policy says that payload does not include business data. Orders are handled for license delivery (email, plan, amount, order time). Card numbers are handled by Stripe and are not stored by VeloTrak.

## How should I read the performance figures?

3,071 clicks per second was load-tested on a shared 4-vCPU VM. The app, PostgreSQL, ClickHouse, and the load generator all ran on that one box. 92,135 clicks were sent and none were lost, which is about 265 million clicks a day at that rate. The 2 vCPU / 4 GB floor is a different, smaller target: at least 800 clicks per second. Numbers shown on the public homepage ledger are samples.

## What exactly is the $399 Founder plan?

All Pro features for life, on 1 install, with 12 months of updates included. Limited to 100, and only during the presale window.

## Can I look before I commit?

Yes. The [live demo](https://demo.velotrak.app/admin/#email=demo%40velotrak.app&password=admin123) is read-only. The email and password are already in the link; click Sign in. There is no sign-up. You can also run the free plan on real traffic. Neither path asks for a card.

## If I let an AI operate through MCP, could it mess things up?

Deletes and edits need two-step confirmation: a diff first, and the change runs only after you approve. Permissions are chosen per area in the UI. Free is read-only. Pro and above can use all 90 tools for read/write. The worked example on the website (editing one lander headline) is illustrative; the tool names there are simplified.

## How do CAPI postbacks work?

Meta, TikTok, and Google are included on every plan.

- Meta: Purchase, Lead, and other events. Each result can be checked.
- TikTok: TikTok Events API.
- Google: GA4 Measurement Protocol.

Free includes one account per platform. Pro removes that cap. Binding priority is campaign, then traffic source, then broadcast.

## Where do I get help?

Email [support@velotrak.app](mailto:support@velotrak.app). Pro includes email support. Team includes priority support. The terms describe support as community, email, or priority depending on the plan. See [SUPPORT.md](../SUPPORT.md).

## Is the software open source?

This GitHub repository does not contain the application source and does not include an open-source license. Use of the software is covered by https://velotrak.app/terms/.
