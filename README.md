# dmit tokyo vps: CN2 GIA vs Tier 1, real monthly prices, and which Tokyo plan is actually worth paying for

Someone searching for a dmit tokyo vps usually has two requirements already figured out. They want a Japanese IP, and they want traffic going to and from mainland China that doesn't collapse at 8pm. The hard part is everything after that: DMIT runs three different network profiles in Tokyo, most of the older blog tables floating around are out of date, and the plan you want is probably showing "out of stock" right now.

Here's the current picture, with prices pulled from DMIT's own order pages rather than from the recycled tables you'll find on most VPS aggregators.

## Why Tokyo, and what it does for Chinese-facing traffic

CN2 GIA is China Telecom's premium international route. Both directions stay on Telecom's own backbone instead of hopping through congested public exchange points, which is why peak-hour performance holds up better than a generic transit line. Putting that route in Tokyo takes advantage of the physical distance: Japan sits close enough to mainland China that round trips commonly land in the 50–90ms range on an optimized route, versus 150ms+ for the US West. Hong Kong is still faster, usually 20–50ms, but Tokyo is where you go when you specifically need a Japanese IP or when Hong Kong pricing doesn't work for your budget.

Four groups of people end up on a Tokyo node:

- Anyone who needs a genuine Japan IP address for regional e-commerce, account registration, or media access
- Projects serving both mainland users and the wider Asia-Pacific region, where a geographically central node makes sense
- Multi-region deployments using Tokyo as the APAC relay
- People who want lower latency than the US but can't justify Hong Kong pricing

If low latency into China is your only goal and the IP country doesn't matter, Hong Kong is still the better answer. Tokyo's value comes from the combination.

## The three Tokyo network profiles, and why one of them is gone

DMIT's Tokyo (TYO) line has historically shipped in three tiers. Only two are still orderable.

### Premium — TYO.AS3.Pro

Return traffic goes out on China Telecom CN2 GIA, with Unicom's AS9929/AS10099 premium route and China Mobile's CMI peering mixed in. Outbound is optimized too, with Telecom and Unicom heading out via CTG GIA and Mobile via CMI. The port is 1Gbps, you get 1 IPv4 plus a /64 IPv6 block, and virtualization is KVM. Traffic overage means the instance pauses.

This is the flagship. It's the plan that makes sense if your users are in China and you care about packet loss and evening stability.

### Eyeball — TYO.AS3.EB

Eyeball routed all three carriers' return traffic over CMI, with CTG GIA outbound for Telecom and Unicom. It was a reasonable middle option at $25.90/month for the TINY tier.

As of the most recent checks, it is no longer listed in DMIT's Tokyo store — several trackers noticed the Tokyo page showing only Premium and Tier 1. Treat it as retired unless it reappears. Don't buy a plan assuming you'll be able to move onto EB later.

### Tier 1 — TYO.AS3.T1

Plain international bandwidth. Telecom and Unicom both go via NTT in each direction, with some routes detouring through the US on Lumen; Mobile uses CMI. There is no China optimization, and DMIT doesn't pretend otherwise.

The trade-off is the traffic policy: instead of pausing when you exceed your quota, T1 throttles you down and keeps you online. That alone makes T1 the better pick for high-volume, low-latency-sensitivity work.

## Every Tokyo plan DMIT currently lists

Prices below are the figures DMIT publishes on its order pages, in USD. Both lines support monthly and longer billing cycles; the monthly figure is the one DMIT advertises, so that's what's shown here.

### Premium (TYO.AS3.Pro) — CN2 GIA return, 1Gbps port

KVM virtualization, AMD EPYC 7003 series, NVMe/SSD storage, 1 IPv4 + 1 IPv6 /64. Traffic overage: instance paused.

| Plan | vCPU | RAM | Storage | Monthly traffic @ port | Monthly price | Order |
| --- | --- | --- | --- | --- | --- | --- |
| TYO.AS3.Pro.TINY | 1 | 1.0GB | 20GB SSD | 500GB @ 1Gbps | $21.90 | [Check TINY availability and current price](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.STARTER | 1 | 2.0GB | 40GB SSD | 1000GB @ 1Gbps | $45.90 | [See the STARTER plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.MINI | 2 | 4.0GB | 60GB SSD | 2000GB @ 1Gbps | $89.90 | [Open the MINI plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.MICRO | 4 | 4.0GB | 80GB SSD | 4000GB @ 1Gbps | $189.90 | [Open the MICRO plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.MEDIUM | 4 | 8.0GB | 160GB SSD | 6000GB @ 1Gbps | $320.90 | [Open the MEDIUM plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.LARGE | 8 | 16.0GB | 320GB SSD | 8000GB @ 1Gbps | $429.90 | [Open the LARGE plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.Pro.GIANT | 8 | 24.0GB | 640GB SSD | 15000GB @ 1Gbps | $829.90 | [Open the GIANT plan](https://www.dmit.io/aff.php?aff=12046) |

Two things stand out. First, the old $39.90 STARTER and $79.90 MINI prices you'll find on a dozen blogs are stale — those tiers have moved up. Second, note how much you pay for memory on this line: going from TINY to STARTER more than doubles the price for 1GB of extra RAM and 500GB more traffic. The Pro line is priced for routing quality, not for resource-per-dollar.

### Tier 1 (TYO.AS3.T1) — international routing, throttled on overage

Same AMD EPYC 7003 generation, 4–10Gbps ports, 1 IPv4 + 1 IPv6 /64. Overage: throttled, never suspended.

| Plan | vCPU | RAM | Storage | Monthly traffic @ port | Over quota | Price | Order |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TYO.AS3.T1.WEE | 1 | 1GB | 20GB | 1000GB @ 4Gbps | 50Mbps unlimited | $36.90/year | [Check the WEE annual plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.TINY | 1 | 2GB | 40GB | 2000GB @ 4Gbps | 100Mbps unlimited | $6.90/month | [See the T1 TINY plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.STARTER | 2 | 2GB | 40GB | 4000GB @ 10Gbps | 100Mbps unlimited | $12.90/month | [See the T1 STARTER plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.MINI | 2 | 4GB | 80GB | 8000GB @ 10Gbps | 100Mbps unlimited | $21.90/month | [See the T1 MINI plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.MICRO | 4 | 4GB | 80GB | 16000GB @ 10Gbps | 200Mbps unlimited | $32.90/month | [See the T1 MICRO plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.MEDIUM | 4 | 8GB | 160GB | 32000GB @ 10Gbps | 200Mbps unlimited | $49.90/month | [See the T1 MEDIUM plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.LARGE | 8 | 16GB | 320GB | 64000GB @ 10Gbps | 500Mbps unlimited | $99.90/month | [See the T1 LARGE plan](https://www.dmit.io/aff.php?aff=12046) |
| TYO.AS3.T1.GIANT | 8 | 24GB | 640GB | 128000GB @ 10Gbps | 1Gbps unlimited | $199.90/month | [See the T1 GIANT plan](https://www.dmit.io/aff.php?aff=12046) |

The WEE plan at $36.90 per year is the cheapest way into a Tokyo DMIT box with a Japan IP. It's also the most oversubscribed-looking deal on paper, so expect it to sell out fast when it restocks.

> Configs and stock shift with each restock batch. Confirm the specs and price on the order page before you pay — this applies to every table on this page.

## The overage rule matters more than the CPU

If you take one thing from the Pro-versus-T1 comparison, make it this: the two lines fail differently when you run out of traffic.

Pro pauses the instance. Your site goes down, your tunnel stops working, and you pay for more traffic or wait for the month to roll over. There's no graceful degradation.

T1 throttles instead. TINY drops to 100Mbps, WEE drops to 50Mbps, and larger plans settle at 200Mbps, 500Mbps, or 1Gbps. You keep running at whatever speed that limit buys you, with no data cap. For a relay node, a backup target, or a service where "slow" beats "offline," that's a meaningful difference. For a customer-facing site where 50Mbps isn't going to cut it, it's not a safety net — it's a slower outage.

## $21.90 vs $6.90: how the decision actually breaks down

The pricing gap between the two Tokyo lines is roughly triple at the entry level, and the hardware specs are nearly identical. What you're buying with Pro is the route.

Reach for **TYO.Pro.TINY** when the people using the server are in mainland China and will notice the difference: a shop or landing page with Chinese visitors, an API where 200ms of added latency is felt, a production service where evening packet loss generates support tickets. TINY's 500GB per month is the real constraint for most people. A single modest WordPress site with caching won't touch it; anything with media delivery or a lot of API chatter will.

Reach for **TYO.T1** when you want the Japan location for its own sake — regional presence, a relay or exit node, batch jobs, a staging environment, anything serving users who aren't routing through Chinese carriers. T1.MINI at $21.90/month buys 8TB of traffic and 4GB of RAM, which is a different product from Pro.TINY at the same price. One gives you a premium route with tight traffic; the other gives you ordinary routing with room to breathe.

The awkward middle is Pro.MINI and above. At $89.90/month for 2 vCPU and 4GB, you're paying almost entirely for the route, and there are cheaper ways to get that much compute in Tokyo. Pro makes sense at this tier only if China-facing quality is a hard requirement and the traffic allowance still fits.

## Stock, restocks, and what actually happens at checkout

DMIT's Tokyo Premium line is genuinely supply-constrained, and it's worth understanding why before you get frustrated with the store page. The company owns its bandwidth commitments rather than reselling, and it positions itself as not overselling capacity. Independent trackers have repeatedly noted that Tokyo restocks come from recycled or released IP addresses rather than new capacity, and DMIT has reportedly told users not to expect large-scale restocks on short notice.

Practically:

- T1 plans have been sold out entirely at several points in recent months, and the Tokyo page occasionally shows nothing orderable
- Pro plans appear in small batches; TINY was showing as out of stock on DMIT's own cart page during recent checks
- There's no reliable waitlist. Restock announcements circulate through community channels, and TYO.Pro batches tend to clear quickly
- If you need the plan by a specific date, order when you see it in stock rather than planning to buy later

Payment options reported by users include Alipay, PayPal, and card payments, with support tickets handled in both Chinese and English. If a card or payment method matters to your decision, verify it on the checkout page — those options change.

## Discount codes: worth trying, not worth trusting

DMIT doesn't run the constant "50% off everything" cycle that lower-tier hosts do. Its discounts are recurring codes tied to a specific product line and billing cycle, usually requiring quarterly or annual prepayment. Codes circulating in the community include a roughly 20% recurring discount on Tokyo/Hong Kong Pro for quarterly and longer terms, and around 30% recurring on Tokyo/Hong Kong T1 for the same conditions, with smaller discounts for monthly billing. Several readers have reported these still validating.

I can't confirm those codes are live right now, and neither can any list you'll find online, including this one — DMIT changes the codes and their product-line scope without much fanfare, and some explicitly exclude the WEE plan. The practical approach: pick your plan and billing cycle first, paste the code into the "Validate Code" field on the order page, and only proceed if it validates. A recurring discount is worth more than it looks, because it applies to renewals rather than just the first invoice.

👉 [Test a promo code against your plan on DMIT's order page](https://www.dmit.io/aff.php?aff=12046)

## Test IPs, hardware, and what third-party reviewers measured

Before buying, you can check the route from your own location. DMIT publishes test addresses per line:

- Tokyo Premium: `154.12.190.32`
- Tokyo Tier 1: `154.31.112.5`
- Looking Glass available at `https://lg.dmit.sh/`

The hardware across the Tokyo lineup is AMD EPYC 7003 series with SSD/NVMe storage. One published review of the now-delisted Eyeball tier recorded roughly 375Mbps down and over 1Gbps up on a 2GB plan, disk I/O around 405MB/s, and average ping of about 131ms across all three Chinese carriers — 84ms via Telecom, 80ms via Unicom, and 232ms via Mobile from the tester's location, with 47ms from Hong Kong/Macau/Taiwan nodes. That's a useful reminder that "China latency" isn't one number: it varies enormously by carrier and city, which is exactly why the test IPs exist.

On streaming: reviewers have found the Tokyo IPs unlocking services like Netflix, TikTok, and Disney+, but DMIT doesn't guarantee this, IPs change, and the tested address was flagged as broadcast rather than residential. Don't build a business on that assumption.

Two operational details worth knowing. Each plan includes 1 IPv4 and a /64 IPv6 block, and KVM virtualization means you can load a custom ISO if you want to. Community trackers also report a blocked-IP replacement policy: one free swap roughly every 15 days for censored addresses, with other swaps charged around $5. Confirm that policy with support before you depend on it — it's the kind of thing that quietly changes.

## Who shouldn't buy a DMIT Tokyo plan

Being honest about the fit saves everyone time.

If you just want cheap CPU and lots of disk, this is the wrong store. Every tier here is priced for network quality, and T1 at $6.90/month is a bargain for bandwidth, not for compute.

If you want the lowest possible latency into mainland China, Hong Kong beats Tokyo on the physics. Tokyo wins when you need a Japan IP and good China routing together.

If your project can't tolerate an outage when traffic runs out, avoid the Pro line entirely unless you're buying enough headroom that you'll never hit the cap. T1's throttling is the more forgiving failure mode.

And if you're planning a deployment months out based on inventory that exists today, don't. Buy the plan when you see it available, or plan around the possibility that it isn't.

## Quick answers to the questions that keep coming up

**Is T1 really unlimited after you hit the cap?** Yes, in the sense that the server stays online with no data limit, but your port speed drops to the plan's throttled rate — 50Mbps on WEE, 100Mbps on TINY through MINI, and up to 1Gbps on GIANT. Unlimited at 50Mbps is a very different thing from unlimited at 1Gbps.

**Why is everything out of stock?** Tokyo restocks are small and depend on IP availability. DMIT has said not to expect large batches soon. Pro plans recycle in and out; T1 has gone fully sold out.

**Can I start on T1 and move to Pro later?** There's no announced upgrade path between network lines, and treating one as a trial for the other is risky given how often Pro is unavailable. Buy the line you actually need.

**Should I get the Eyeball plan?** You likely can't — it's not showing in the Tokyo store right now. If it returns, it slotted between Pro and T1 for Mobile-heavy traffic, but plan around what's orderable today.

**Is Tokyo or Hong Kong the better pick?** Hong Kong for pure China latency and for users concentrated in the south. Tokyo when you need a Japan IP, when you're serving both China and wider Asia, or when Hong Kong's price premium is the deciding factor.

the bottom line for most readers looking at a dmit tokyo vps: if the audience is in China and the workload is light, TYO.AS3.Pro.TINY at $21.90/month is the plan to watch for and buy the moment it restocks. If you need volume, a Japan exit, or a node that survives a traffic overage, T1.TINY at $6.90/month or T1.MINI at $21.90/month does the job for a fraction of the cost — just don't expect the route to behave like the Premium line.

👉 [See what's currently in stock and order a Tokyo plan](https://www.dmit.io/aff.php?aff=12046)
