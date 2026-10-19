# MakerMap reverse-engineering case: portable identity / mymcp.id

**Case date:** 2026-10-19  
**Target:** https://www.makermap.lol/JamesWonX?v=blfq8z  
**Reference homepage:** https://www.makermap.lol/  
**Analyst question:** Which MakerMap interaction, visual, social-discovery, matching and MCP patterns can inform a platform-independent network of consent-based human and business agents?

## Integrity / evidence status

This document is an **evidence-based reconnaissance dossier, not a completed REA runtime capture**.

- **Observed through publicly accessible MakerMap pages:** text/controls/navigation of the homepage, About, MCP and other indexed public profile/product pages; documented product/identity/security/data flows.
- **Observed in a public marketing visual:** Product Hunt image showing desktop maker directory, dark high-contrast promotion, and mobile map with photographic avatar markers. This is a promotional image, **not** a screenshot of the exact JamesWonX URL or a verified live viewport.
- **Not captured yet:** the exact JamesWonX rendered profile, authenticated flows, JavaScript bundles, DOM structure at runtime, network requests and responses, map renderer/runtime, responsive screenshots, performance, and private state.
- **Blocker here:** REA was not available as an active MCP runtime, the sandbox cannot resolve the target hostname, and web retrieval of the exact JamesWonX path was unavailable. Do **not** describe the findings below as REA-captured, or as recovered proprietary source.
- **Next step:** run the supplied REA capture scenarios from a connected machine with a current Node and Chrome-family browser; append unmodified Evidence IDs/outputs, timestamps and tool versions.

## 1. CONFIRMED behavior and presentation

| Surface | Confirmed information | Source |
|---|---|---|
| Landing / navigation | 'Explore', 'Makers', 'Meetups', 'Community', 'You'; additional 'Products', 'MCP', 'MakerMapBot', 'Lists', 'Cities', 'Sponsor a boat', points information. Map controls include +, − and fullscreen; search input reads 'Search or ask the map'. | https://www.makermap.lol/ |
| Discovery | Location + interest/sector search; maker markers on global map; makers grouped by cities; public maker pages link profiles and projects. | https://www.makermap.lol/ ; https://www.producthunt.com/products/makermap |
| Maker profile | Name/X handle; public bio and city/country; projects, tags, working style, people they want to meet, connection/maker-met counts, points and profile claims; profile tabs on sampled public profiles: Overview, Posts, Network, Points. | https://www.makermap.lol/tuhel ; https://www.makermap.lol/mpaepper |
| Identity and acquisition | Accounts depend on X sign-in and a claim post. Source data includes public X intro/profile content, social engagement and linked products; people can ask for removal. City-level location is shown publicly, not precise addresses. | https://www.makermap.lol/privacy |
| Classification | Public policy says the product uses Jev through OpenRouter/TypeSafe to classify public intros and compute match scores; includes stage, interests, roots and desires. | https://www.makermap.lol/privacy |
| Operator / stack | Public policy lists Vercel, TikHub, X, Stripe, Resend, DataFast, PostHog and OpenRouter. This is a **vendor declaration**, not network-verified identification. | https://www.makermap.lol/privacy |
| MCP | Public documentation names a remote MCP endpoint at https://www.makermap.lol/mcp, streamable HTTP, OAuth 2.1 + PKCE, one-hour access tokens, rotating refresh tokens and interactive MakerMap-styled responses. Documentation describes 20 model-accessible operations and 10 screen-button operations. | https://www.makermap.lol/mcp |
| Agent actions | Tools include find_makers, get_maker, search_makers, similar_makers, find_products, event creation/RSVP, draft_post, community and settings. Proposed changes generally require user tap-to-confirm; posting to X requires action on X. | https://www.makermap.lol/mcp |
| Commercial model | Public policy describes optional paid profile pins and sponsored boats through Stripe. | https://www.makermap.lol/privacy |
| Visual reference | Public launch image presents a dark/high-contrast desktop list and mobile map with person/avatar pins and compact profile cards. Does **not** establish exact colors, layout or interactions for the requested profile page. | https://www.producthunt.com/products/makermap ; image https://ph-files.imgix.net/d9701f1c-1a2b-448b-9494-4a40b96c04d4.png |

**Caution:** MakerMap **already has an MCP connector and some supported operations**. It is inaccurate to characterize it as 'a static X map with no agent access'. The meaningful missing/unknown capabilities are separate portable mutual relationship proofs, agent-to-agent communication across independent identities/providers, and independent verified business offer/booking endpoints. We have not proved the complete absence of unpublished features.

## 2. INFERRED system architecture (requires runtime confirmation)

Likely public pipeline (based on privacy statement, MCP documentation, and launch materials):

```text
Public X intros/profiles and linked product URLs
   -> external data provider (TikHub, declared)
   -> classification/match features (Jev via OpenRouter, declared)
   -> persistent maker/project/location records (Vercel, declared)
   -> map, directory, profile, recommendation, event, community views
   -> OAuth 2.1 MCP gateway + interactive confirmation screens
   -> X posts, site-local follows/events/profile changes, email and billing
```

This is a **logical reconstruction**, not observed database schema, deployed service topology, protocol trace, route inventory or recovered proprietary code. Determine actual JS bundling, map service, endpoints and search mechanisms with REA captures before making implementation claims.

### Visible interaction inventory to test with REA

1. Enter maker profile using the exact supplied link; capture wide desktop and phone viewport, visual hierarchy and link destinations.
2. Home map: wait for marker load, pan/zoom, select marker, select a city and compare DOM and network; determine cluster behavior and map rendering technology.
3. Search: 'AI builders near Windsor', 'designer building Android apps', a specific handle. Record empty/error/loading states and semantic vs keyword differences.
4. Switch Makers / Products / Meetups / Community and profile tabs. Record how search state, location and selection persist.
5. Profile claim and 'Log in with X': record public UI up to authorization, **do not submit credentials**, click buy buttons, or mutate an account.
6. Inspect MCP public docs separately from auth handshake; read OAuth metadata only where publicly exposed. Do not send authenticated tokens to a report.
7. Responsive/mobile: compare list-first, map-first, drawer/overlay behavior; collect screenshots and accessibility snapshots at 390px and 1440px.
8. Capture interaction timings, request initiators and JSON **shapes**; do not assume a response body or internal API from marketing copy.

## 3. Interface elements worth reinterpreting for mymcp.id

**KEEP THE PATTERN, not the branding or source:**

- Geo-first exploration with fast map/list switching and semantic search.
- Dense, scannable profile rows with avatar, location, verified state, skill/industry tags, current projects and stated intention.
- City/category indexes as SEO and discovery entry points.
- Real-time-feeling, searchable maker and product profiles with simple share URLs.
- Contextual 'people worth meeting' cards showing *why* a match fits.
- An MCP read layer returning useful structured results, with typed interactive confirmations for state-changing actions.

**CHANGE the operating primitive:**

- MakerMap: public X persona + social/posts + matching -> introductions often via X.
- mymcp.id: World-authenticated human with separate portable identifier + privacy preferences + mutual connections + authorized agent capabilities -> reciprocal introductions and verified bookings.
- MakerMap: one site's remote MCP gateway for the MakerMap directory.
- mymcp.id: a protocol-capable agent directory with independently addressable human/business identities and narrowly scoped actions (can initially be implemented as a **single multi-tenant gateway**, not one physical server per user).
- MakerMap: follower/point/rank signals and platform-controlled listing.
- mymcp.id: mutual, revocable relationship state, consented reachability, auditable actions and portable export; do not gamify a connection into a tradable token.
- MakerMap: X-authenticated audience of makers.
- mymcp.id: people *and* local businesses; individual location aggregated/coarse by default and businesses opt into precise pins.

### Suggested screen translation

| Inspiration | mymcp.id screen | User action |
|---|---|---|
| Global discovery map | Explore | Filter verified people or businesses by region, industry, availability and intent |
| Maker directory | People | Discover selectively visible human profiles and compatible intentions |
| Project/product list | Offers | Browse services, appointment slots, quote requests and relevant products |
| Maker profile | Portable ID card | View public claims, capability availability, QR link and privacy-safe identity proof |
| Find my matches | Agent proposals | Ask 'who can help build my Android app?' and receive reciprocal reasons |
| Event / RSVP | Introductions and calendar | Both people approve a proposal; authorized agent finds mutually allowed slot |
| MCP connector | Agent gateway | Read available actors/offers; propose with scope/expiry; confirm booking with receipt |

### Privacy-first location model

- **Individuals:** display regional clustering/counts publicly, and exact location only with explicit mutual consent; do not expose GPS as an identity proof. A unique face/avatar pin next to an exact home coordinate is dangerous.
- **Businesses:** visible exact commercial address only if owner opted in and location has been verified through a business-claim process.
- **World ID:** proof of unique personhood, **not** proof of legal identity, address, business ownership or professional competence.
- **Connections:** bilateral approvals, independently verifiable signed relationship proofs as a possible future design, revocation, separate agent permissions, selective disclosure, explicit capability expiry.
- **Do not** put contact graphs, GPS traces or sensitive profile fields on a public blockchain.

## 4. Reference conceptual records (NOT MakerMap's recovered schema)

```text
Identity: id, public_handle, verifier_method, verification_reference,
          published_fields, display_region, discovery_opt_in
Relationship: id, party_a, party_b, accepted_by_a, accepted_by_b,
              portable_attestation_ref?, revoked_at, disclosure_rules
AgentPermission: actor, grantee, capability, scope, expires_at,
                 requires_confirmation, revocable_at
Intent: person_id, need, timeframe, region_preference, visibility, expiry
Offer: business_id, action_type, public_description, availability_source,
       booking_capability_ref, price_policy?
Proposal: intent_id, candidate_id, mutual_fit_explanation, approvals, state
Booking: proposal_id, provider_ref, timestamp, confirmation_ref, receipt
```

Optional fields marked `?` are **design placeholders**. V1 does not require blockchain, public relationship proofs, escrow, tokenized contacts or per-user physical MCP deployments.

## 5. Competitive assessment

**MakerMap's true advantage:** its discovery loop starts with an existing public corpus and native sharing/distribution on X. It also has credible UX, multiple local/network engagement loops, and an already described MCP surface. Replicating every feature on day one would be a mistake.

**mymcp.id's potential advantage (hypothesis):** the relationship and the ability to contact/act can persist when a platform, agent provider or host changes; a verified business can publish an actionable offer; the AI can propose an introduction and complete a consented appointment. These are only advantages **if** migration, revocation and booking completion are reliable in real use.

**Weakest assumption:** portable verified identity itself creates growth. It does not. The immediate benefit must be a successful introduction or business booking, with the portability promise becoming valuable through repeated use.

## 6. Build order and acceptance tests

1. Windsor / builders: World-authenticated people, coarse discovery, intentions, contextual matching, mutual acceptance and 15/30-minute calendar booking.
2. Windsor / businesses: owner-claimed business page and exact location, one standardized bookable offer, provider-backed slot check and confirmed booking receipt.
3. Portable mutual connections: export independently usable proofs/reachability information with consent; revocation works even after a provider change.
4. One multi-tenant MCP gateway with scoped capabilities and audit; expand integrations only after the first two transactions work.

**Acceptance test A:** Two unrelated verified people can discover each other from stated intention, both explicitly accept, schedule and successfully meet.

**Acceptance test B:** A person can find a Windsor business, have an agent request a permitted service/slot and receive a real confirmation from its booking provider.

**Acceptance test C:** Connection stays addressable after switching UI client or AI provider; permission expiry and revocation actually prevent further agent actions.

## 7. REA runnable captures: next evidence pass

This REA fork documents browser observation in [docs/browser-observation.md](../../docs/browser-observation.md) and declarative scenarios in [docs/browser-scenario-contract.md](../../docs/browser-scenario-contract.md).

Prerequisites: a connected machine, installed Chrome/Chromium, Node 22.19+ or another supported release, and REA CLI. Use `npx -y rea-agents@latest` or install `rea-agents` globally. Update `browser.executable_path` in both JSON scenarios for your OS.

```bash
npx -y rea-agents@latest capture-browser-scenario \
  research/makermap/profile-capture.json --json \
  > makermap-profile-evidence.json

npx -y rea-agents@latest capture-browser-scenario \
  research/makermap/home-capture.json --json \
  > makermap-home-evidence.json
```

For a **manual interactive** capture, open Chrome using a dedicated profile on `127.0.0.1:9222` (do not expose the port), then discover the target and pass its ID:

```bash
npx -y rea-agents@latest list-browser-targets http://127.0.0.1:9222 --json
npx -y rea-agents@latest inspect-web-page http://127.0.0.1:9222 TARGET_ID \
  --observation-ms 10000 --include-accessibility-text \
  --include-json-body-shapes --json
npx -y rea-agents@latest analyze-web-bundle http://127.0.0.1:9222 TARGET_ID --json
npx -y rea-agents@latest capture-web-screenshot http://127.0.0.1:9222 TARGET_ID --json
```

Start capture **before** clicking/searching/zooming. Network requests that ran before REA attached are not captured by a subsequent observation. Use unmodified JSON Evidence, fresh screenshots, tool versions, timestamp and selected URL to promote an inference to an observation. Redact any account/session identifiers before sharing evidence.

## Public sources / provenance

- Requested exact target: https://www.makermap.lol/JamesWonX?v=blfq8z (runtime inaccessible here).
- Main nav/home text: https://www.makermap.lol/
- About / reported maker/product counts and activities: https://www.makermap.lol/about
- Published MCP architecture, tools, safety: https://www.makermap.lol/mcp
- Data provenance, identity, ranking and vendor declarations: https://www.makermap.lol/privacy
- Public example profiles: https://www.makermap.lol/tuhel ; https://www.makermap.lol/mpaepper
- Launch and promotional visuals: https://www.producthunt.com/products/makermap
- REA browser guide: https://rea.tools/guides/browser/

**No source code of MakerMap has been copied into this repository.**
