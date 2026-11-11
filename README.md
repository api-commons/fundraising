# Nonprofit Fundraising

The common fundraising vocabulary -- the donors and constituents who give, the donations and gifts they make, the pledges and recurring gifts they commit to, the campaigns that ask and the funds the money is designated to -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Non-Profit, Nonprofit, Fundraising, Donations, Philanthropy, Charity, Donor Management, Giving in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| donor | 6 | 6 | email 100%, first_name 100%, id 100%, last_name 100%, created_at 83%, phone 83%, address 50%, gender 50%, name 50%, organization_id 50%, updated_at 50% | supporters 3, constituents 2, constituent 2, donors 2 |
| donation | 11 | 11 | id 73%, amount 64%, metadata 64%, created_at 55%, donor_id 55%, type 55% | donations 7, gifts 2, contributions 2, gift 1 |
| fundraising_campaign | 6 | 6 | created_at 100%, id 100%, name 100%, goal 83%, end_date 67%, status 67%, updated_at 67%, currency 50%, start_date 50% | campaigns 6, appeals 2, fundraisers 2, fundraiser 1 |
| fund | 5 | 5 | id 100%, name 100%, created_at 80%, updated_at 80%, campaign_id 60%, description 60%, is_default 60% | designations 4, funds 2, fund 2, designation 1 |

Cohort: 50 providers with harvested OpenAPI, 14 crosswalks. Of the providers exposing a donor: 83% create, 83% list, 100% fetch, 67% update, 50% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Fundraising publishes little (50 providers, 14 mapped), but what is published agrees almost completely: a donation on amount, type, donor and date; a campaign on name, goal, currency, start and end; a donor on name, email, phone and address; a fund on name, description and the campaign it belongs to.
- Nonprofit software converged on one model of giving -- the donor, the gift, the appeal and the fund -- and the published APIs carry it with little drift.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Constituents and supporters are donors; gifts and contributions are donations; designations are funds.
- Campaigns are `/fundraising-campaigns`: email marketing and advertising own `/campaigns`.
- Donations need no donor resource in the same API: gift-processing platforms expose gifts alone.
- Pledges were measured and dropped.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
