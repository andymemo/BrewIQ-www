# Welcome to the BrewIQ Docs

BrewIQ is a web app for home and small-scale craft brewers, covering the full lifecycle of a beer - from recipe design through scheduling, brewing, fermentation, packaging, and stock. It learns from your brew logs over time and offers guidance (like brewhouse efficiency or mash pH correction) based on your own history.

This is the end-user reference for BrewIQ. Use the navigation to jump to a topic, or start here:

- **[Getting Started](getting-started.md)** - creating your account, signing in, and two-factor authentication
- **[Dashboard](dashboard.md)** - your home screen overview
- **[Recipes](recipes.md)** - building, organizing, and sharing recipes
- **[Brew Sessions](brew-sessions.md)** - brewing, fermentation tracking, and packaging
- **[Inventory](inventory.md)** - your grain, hop, yeast, and adjunct catalogue, with your own prices
- **[Stock](stock.md)** - packaged beer and raw ingredient lots on hand, with a full audit trail
- **[Planning](planning.md)** - equipment, the brewing schedule, and blocked days
- **[Devices](devices.md)** - connecting Tilt/iSpindel/RAPT Pill gravity sensors and Grainfather temp control
- **[Accounts](accounts.md)** - customers and excise duty reporting for commercial breweries
- **[Account & Preferences](account-preferences.md)** - units, defaults, and your profile
- **[Tenant Administration](tenant-administration.md)** - managing your brewery's users, roles, and settings
- **[FAQ](faq.md)** - common questions

## A batch from recipe to excise report

This is the life of one batch, and where each step is covered in these docs. Click any box to jump to it.

```mermaid
%%{init: {"flowchart": {"curve": "linear"}}}%%
flowchart TD
  RM["Receive Stock: raw ingredient lot"]
  subgraph PLAN["Plan<span style='display:inline-block;width:280px'></span>"]
    R["Recipe"] --> BI["Brew it!, or right-click a day on the Planning schedule"]
    BI --> NS["New brew session: batch number, brew date, snapshot, fermenter"]
    NS --> FREE{"Fermenter free?"}
    FREE -- "No" --> NS
    FREE -- "Yes" --> PL["Planning: vessel booked on the timeline"]
  end

  subgraph BREW["Brew #amp; ferment<span style='display:inline-block;width:403px'></span>"]
    PL --> BR["Brewing: brew day logs"]
    BR --> PF["Primary fermentation"]
    PF --> SF["Secondary fermentation"]
    SF --> CO["Conditioning"]
  end

  subgraph PACK["Package<span style='display:inline-block;width:254px'></span>"]
    CO --> MP["Mark Packaged"]
    MP --> PK["Packaging tab: volume, costs, packaged items, Final ABV"]
    PK --> SS["Save to Stock"]
  end

  subgraph STOCK["Stock<span style='display:inline-block;width:540px'></span>"]
    PS["Packaged product on hand"]
    PS --> MV{"Record a movement"}
    MV --> OUT["Sold, Given away, Consumed"]
    MV --> LOSS["Written off, Spoiled"]
  end

  subgraph ACC["Accounts<span style='display:inline-block;width:246px'></span>"]
    EX["Excise and alcohol levy report"]
  end

  SS --> PS
  DEV["Tilt, iSpindel, RAPT Pill, Grainfather"] -. "readings" .-> PF
  RM -. "assign lot to a recipe row" .-> BR
  OUT --> EX

  classDef external fill:#c8620e0d,stroke:#c8620e,stroke-width:1.5px,stroke-dasharray:4 3
  classDef step fill:#c8620e26,stroke:#c8620e,stroke-width:1.5px
  classDef decision fill:#c8620e59,stroke:#c8620e,stroke-width:1.5px
  classDef outcome fill:#c8620e26,stroke:#9b1900,stroke-width:3px
  class R,BI,NS,PL,BR,PF,SF,CO,MP,PK,SS,PS,OUT,LOSS step
  class FREE,MV decision
  class EX outcome
  
  class DEV,RM external
  style PLAN fill:none,stroke:#c8620e,stroke-dasharray:6 4
  style BREW fill:none,stroke:#c8620e,stroke-dasharray:6 4
  style PACK fill:none,stroke:#c8620e,stroke-dasharray:6 4
  style STOCK fill:none,stroke:#c8620e,stroke-dasharray:6 4
  style ACC fill:none,stroke:#c8620e,stroke-dasharray:6 4

  click R href "recipes/" "Recipes" _self
  click BI href "brew-sessions/#starting-a-session" "Starting a session" _self
  click NS href "brew-sessions/#starting-a-session" "Starting a session" _self
  click FREE href "planning/#how-long-does-a-batch-occupy-a-vessel" "Planning" _self
  click PL href "planning/" "Planning" _self
  click BR href "brew-sessions/#logs-tab-brew-day-logs" "Brew day logs" _self
  click PF href "brew-sessions/#fermentation-tab" "Fermentation" _self
  click SF href "brew-sessions/#fermentation-tab" "Fermentation" _self
  click CO href "brew-sessions/#session-status" "Session status" _self
  click MP href "brew-sessions/#session-status" "Session status" _self
  click PK href "brew-sessions/#packaging-tab" "Packaging" _self
  click SS href "brew-sessions/#packaging-and-stock" "Packaging and stock" _self
  click PS href "stock/#packaged-product" "Packaged product" _self
  click MV href "stock/#opening-an-item" "Recording movements" _self
  click OUT href "stock/#opening-an-item" "Recording movements" _self
  click LOSS href "stock/#opening-an-item" "Recording movements" _self
  click EX href "accounts/#excise" "Excise" _self
  click RM href "stock/#receiving-stock" "Receiving stock" _self
  click DEV href "devices/" "Devices" _self
  click RM href "stock/#receiving-stock" "Receiving stock" _self
```
