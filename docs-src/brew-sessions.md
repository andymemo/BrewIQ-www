# Brew Sessions

![The Brew Sessions list showing recipe, batch number, brew date and status](images/brew-sessions-list.png)

A brew session is a record of one actual batch — brewed from a recipe, tracked through fermentation, and closed out at packaging. There's no "New Brew Session" button on the sessions list itself; every session starts from a recipe's **Brew it!** action (recipe builder, the recipes list, or a recipe's print preview), or by right-clicking a day on the [Planning](planning.md#starting-a-brew-from-the-schedule) schedule and choosing **New brew session**.

## Starting a session

![The New Brew Session setup screen with Batch Number, Brew Date, and the snapshot checkbox](images/brew-session-setup.png)

**Brew it!** takes you to a short setup screen — deliberately minimal, with no batch scaling:

- **Batch Number** — auto-suggested based on the brew date, editable
- **Brew Date** — defaults to today
- **Take a snapshot of this recipe** (checked by default) — freezes the grain bill, hop schedule, adjuncts, yeast, and mash steps as they are right now, so later edits to the recipe won't change this session's record

- **Assign equipment** (if you have planning permissions) — reserves a vessel on the [Planning](planning.md) timeline for this session.

![The New Brew Session screen with Assign equipment ticked, a Fermenter picker, and a warning that the chosen fermenter is already occupied](images/brew-session-assign-equipment.png)

When you tick **Assign equipment**, choose a **Fermenter**. BrewIQ works out how long the batch will occupy it from the recipe's fermentation steps and checks the vessel is free over that period. If it's already booked, you'll see which batch is in the way and **Create Brew Session** is disabled until you pick a different fermenter or brew date. If the beer will move to another vessel to condition, tick **Transfer to a separate vessel for conditioning** and pick that vessel too.

If the brew date you choose is one of your [blocked days](planning.md#blocked-days), you'll see a warning — you can still go ahead.

Click **Create Brew Session** to open the session detail page. Deleting a session also frees any equipment it had reserved.

Device pairing (a Grainfather controller, a Tilt or similar gravity tracker) isn't part of this setup — you link a device to a session from the [Devices](devices.md) page instead.

## Session status

Every session moves through a fixed sequence: **Planning → Brewing → Primary Fermentation → Secondary Fermentation → Conditioning → Packaged**, shown as a stepper at the top of the session page. Planning and Brewing advance automatically based on the brew date; the fermentation stages advance based on your logs and readings, or manually:

- **Move to Conditioning** — available once you're brewing
- **Mark Packaged** — available once in Conditioning; this also turns off any fermentation-alert email notifications for that session
- **Revert** — undo the last status change (from Packaged back to Conditioning, or from Conditioning back to wherever your logs/readings support)

## Overview tab

Batch Number and Brew Date are editable here (Brew Date locks once fermentation has started). Also shows who created the session and when.

## Logs tab — Brew Day Logs

![The Brew Day Logs tab showing Mash Complete, Pre-Boil, Post-Boil and Fermenter entries](images/brew-log.png)

Records what happened on brew day itself. Each log has a **Log Type** — **Mash Complete, Pre-Boil, Post-Boil, Fermenter** (each loggable once per session), or **Sample** (loggable any number of times) — plus **Wort Volume**, **Wort Gravity**, optional **pH**, and a comment.

Once you've logged a Pre-Boil reading, BrewIQ calculates your actual **Brewhouse Efficiency** for the batch and shows it next to the recipe's expected efficiency, so you can see immediately how the brew day tracked against plan.

Logs lock once the session reaches Conditioning.

## Recipe View tab

A snapshot of the recipe as brewed — grain bill, hop schedule (with the same stage breakdown as the recipe builder), adjuncts, yeast, mash steps, and notes. If you took a snapshot at setup, this reflects the recipe exactly as it was then, even if you've since edited the original recipe.

The one exception is hop alpha acid: if you correct a hop's **Alpha %** in the recipe, BrewIQ copies the correction onto that recipe's open (not yet Packaged) snapshotted sessions, so the batch's IBU stays right.

### Prices on the Recipe View

Grains, hops, adjuncts and yeast each show a price. On a snapshotted session you can:

- Click the **$** button on a row to **override** its price for this batch (with an option to apply it to every row of the same ingredient).
- Click the **refresh** icon on a row to pull your brewery's current [Inventory price](inventory.md#setting-your-own-price) for that ingredient.

Prices set here belong to the session and can differ from the recipe's. They feed the session's cost, and you can still correct them after the session is Packaged — then use **Update Stock** on the Packaging tab so the corrected cost reaches your stock (see below).

### Linking stock to a brew session

If you track [Raw Materials stock](stock.md#raw-materials), you can record which lot an ingredient came from. On a grain, hop, adjunct or yeast row, click the **link** icon in the **Stock Lot** column.

![A session's Grain Bill with a Stock Lot link button on each row](images/session-grain-bill-stock-lot.png)

![The Assign Stock Lot dialog with a dropdown of lots and how much of each is on hand](images/session-assign-lot-picker.png){ width="560" }

Pick a **Lot** from the list (each shows what's on hand) and enter the **Quantity Consumed**. BrewIQ suggests a sensible amount from the recipe, but you can change it to what you really used.

![The Assign Stock Lot dialog showing Lot and Quantity Consumed fields with Clear assignment, Cancel and Save changes](images/session-assign-lot.png){ width="420" }

Saving deducts that quantity from the lot, records it in the lot's history so you can later see every brew it went into, and sets the row's price from the lot's purchase price. **Clear assignment** puts the quantity back. If the session wasn't snapshotted, BrewIQ asks you to take a snapshot first so the ingredient rows exist to link.

## Fermentation tab

This is where day-to-day tracking happens, combining manual entries with any linked devices.

![The Fermentation Tracking gauges, status stepper, and Fermentation Steps schedule](images/fermentation-tracking.png)

**Fermentation Tracking** header — shows four gauges: **Specific Gravity** (with target FG), **ABV (calculated)**, **Fermenter Temp** (flags whether you're in, below, or above the ideal range), and **Attenuation**. If you've linked a gravity-tracking device or temp controller, its data feeds these gauges automatically — whichever source (manual or device) is more recent wins.

**Add Reading** — log Date & Time, Gravity, Temp, pH, and Vessel (Primary/Secondary) by hand at any point.

**Readings table** shows every reading with its source (Manual, or the device it came from). You can select and bulk-delete readings.

**Fermentation chart** — plots gravity, temperature (per source if you have more than one), pH, session target temp, and attenuation velocity over time. Needs at least two readings to appear, and you can drag to zoom.

![The fermentation chart plotting gravity, temperature and attenuation velocity over time](images/fermentation-chart.png)

Everything on this tab locks once the session is Packaged, but stays visible.

### Fermentation Steps — the schedule

This is a step-by-step temperature schedule you build for the batch: name, duration, start temp, and (optionally) a ramp to a finish temp, with an optional Temp Controller mode (Off / Heating & Cooling / Heating Only / Cooling Only) per step.

Turn on **Managed Mode** and BrewIQ pushes each step's target temperature (and heating/cooling mode) to a paired temp controller automatically as the schedule advances — no manual adjustment needed on the controller itself.

Each step can also **auto-advance**: set a condition based on average attenuation velocity dropping below a threshold, average gravity dropping below a threshold, or both, evaluated over a configurable time window, and BrewIQ moves to the next step on its own once the condition is met. You can also **Skip** the active step forward manually, or **Rewind** back to the previous one.

![The Add Fermentation Step dialog showing duration, temperature, and auto-advance conditions](images/fermentation-step-dialog.png){ width="420" }

Rather than typing every step each time, click **Add from template** to apply one of your saved [fermentation profiles](recipes.md#fermentation-profile-templates). If steps already exist you can **Replace** them (only before fermentation starts) or **Add to end**.

Once the session reaches Conditioning, the step list becomes read-only and is replaced by a single flat **Conditioning Temp** field.

## Packaging tab

![The Packaging tab showing Volume Packaged, Batch Costs, and Packaged Items](images/packaging.png)

The tab also holds **Final ABV** — see below.

Available once a session is marked Packaged. This tab tracks **costs and package counts**, not fermentation results — final ABV/attenuation are read from the Fermentation gauges and Overview, not re-entered here.

- **Volume Packaged** — how much liquid you actually collected, with a live cost-per-unit figure calculated alongside it.
- **Batch Costs** — a running list combining ingredient costs pulled in automatically from the recipe plus any manual charges you add (use a negative amount for losses like spillage). You can also **Apply Template** to pull in a saved cost bundle from [Inventory](inventory.md)'s Misc tab.
- **Packaged Items** — log what you packaged it into (Keg / Can / Bottle / Other), with count and volume each; BrewIQ flags if your package totals don't match the Volume Packaged figure so you can catch mistakes.
- **Final ABV** — the ABV recorded for this batch. See below.

### Final ABV

Final ABV is pre-filled with a figure calculated from your actual gravity readings (or the recipe's estimate if there aren't enough readings, which is flagged). It's required, and you can change it. If you enter a value that differs from the calculated one, BrewIQ records the change — who, when, the calculated and entered values — and you can review it from the **history** icon beside the field. This ABV is the one used for [excise reporting](accounts.md#excise).

### Packaging and stock

Below Packaged Items, a **Stock** card links the batch to your [Stock](stock.md) page.

![Packaged Items and the Stock card showing each package line as saved to stock with on-hand counts](images/packaging-stock.png)

Stock is never created automatically. When your package lines are right, click **Save to Stock** and each one becomes a [Packaged Product](stock.md#packaged-product) row, with its cost per unit recorded. The card then shows, per line, how many were **Packaged** and how many are still **On Hand**, with a **Saved to stock** badge; **View Stock** jumps to the Stock page.

If you change something afterwards, the line is flagged and a button appears:

- **Package line changed** or **Cost changed** — click **Update Stock** to bring the stock row in line. A corrected count is recorded as an adjustment, and a corrected cost applies to every unit from that line, including ones already sold. It's refused if the corrected count would be lower than what has already left stock.
- **Apply ABV to All** — appears if a stock item's ABV differs from the session's current Final ABV (for example after you corrected it). It's never applied automatically, because it changes ABV on stock that may already be in a filed excise period.

This tab is read-only outside the Packaged status, so if you revert a session back to Conditioning, your packaging data is preserved but locked until you mark it Packaged again.

## Notifications

Turn on **Gravity alerts** and/or **Temperature alerts** in [Account & Preferences](account-preferences.md) to reveal a bell icon on individual sessions (available while a session is in Primary Fermentation, Secondary Fermentation, or Conditioning) — click it to get emailed about that specific batch.
