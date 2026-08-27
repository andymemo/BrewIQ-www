# Inventory

Inventory is your **ingredient catalogue** — the specs and pricing for grains, hops, yeast, and adjuncts that you pull into recipes. It is **not** a stock-tracking system: there's no "quantity on hand" field, and using an ingredient in a recipe or brew session doesn't deplete anything here. Think of it as your reference library of ingredients, not a pantry counter.

The page has tabs for **Grains**, **Hops**, **Fermentables**, **Adjuncts**, and **Yeasts**, plus a **Misc** tab if you have packaging-cost permissions (covered at the bottom — it's unrelated to recipe ingredients).

Every ingredient you see is either part of the **shared catalogue** (managed by your provider) or a **custom** item you've added yourself. If you only have read access, you can browse the catalogue but not add to it.

## Fields per category

- **Grains** — Type (Base/Special/Acidulated/Crystal/Roasted/Smoked), Colour, Extract (PPG), Origin, Supplier, Recommended usage, Description, Price.
- **Fermentables** — same shape as Grains, plus a Usage tag (Mash/Boil/Late addition/Whirlpool/Ferment/Post ferment) and a Type of Powder/Liquid/Extract. (Grains and Fermentables are two separate categories, not one nested in the other — use whichever fits how you think about the ingredient.)
- **Hops** — Usage (Bittering/Aromatic/Whirlpool/Dry hop), Type (Pellet T90/Pellet T45/CO2 extract/Oil), Alpha Acid % (required), and optional Cohumulone %, Total Oils, Beta Acid %, Origin, Supplier, Description, Price.
- **Adjuncts** — the simplest schema: Usage, Type (Powder/Liquid/Extract/Acid), Supplier, Description, Price. No colour or extract fields.
- **Yeasts** — the richest schema: Code, Style, Type (Dried/Liquid), Flocculation (High/Medium/Low), Alcohol tolerance (High/Medium/Low), STA1 status (Positive/Negative/Unknown), Min/Max/Recommended Temp, Min/Max/Recommended Attenuation %, Description, Price.

## Adding a custom ingredient

Click **Add custom grain / hop / fermentable / adjunct / yeast** at the top of the relevant tab. Start typing the name — if something close already exists in the shared catalogue, BrewIQ shows you matches with a **Clone & customize** button, so you can start from an existing item instead of from scratch. If nothing matches (or you'd rather not use a match), click **Create from scratch** to open a blank form and fill in the fields above.

Custom items you own get full **Edit**/**Delete** icons. Shared catalogue items you don't own only offer a **Clone** icon — cloning makes an editable tenant-owned copy immediately, no confirmation step.

Click any ingredient's name to open a read-only details view without editing it.

## Deleting

Click the trash icon to delete a single item — you'll get a "This can't be undone" confirmation. To delete several at once, select their checkboxes (2+) and use the **Delete N selected** button that appears above the table.

## Finding things

- **Search** by name at the top of each tab.
- **Tag filters** — click the chip badges (Type, Usage, Style, etc.) above the table to filter; multiple chips within one group are OR'd together, different groups AND together.
- **Column filters and sorting** — column headers are sortable, and there are additional dropdown filters (e.g. Origin, Supplier, Source) depending on the category.
- **Columns** button — show/hide table columns; some less-common fields (like Description) are hidden by default to keep the table compact.

## Misc tab (packaging costs, not ingredients)

If you have packaging permissions, a **Misc** tab appears with two unrelated tools used only from a brew session's Packaging step (see [Brew Sessions](brew-sessions.md)):

- **Misc Cost Items** — reusable line items for things like shipping, cleaning, or electricity, each with an optional default amount.
- **Cost Templates** — bundle several Misc Items into a reusable set (e.g. "64L Batch") you can apply to a brew session's costs in one click, either by typing lines manually or picking from your Misc Items.
