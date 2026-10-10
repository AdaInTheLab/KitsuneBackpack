# KitsuneBackpack

A 136-slot backpack for 7 Days to Die V3.3 that keeps the vanilla locked-slot progression instead of handing you everything at spawn.

- **Bag size:** 45 to 136 (8 columns x 17 rows, scrolling)
- **27 slots free at spawn**, the rest show as locked spaces, just like vanilla
- **Pack Mule** unlocks ~22 slots per level: a full 136 at level 5 (pocket mods still work on top)
- God mode and steroids unlock the whole bag
- Encumbrance penalty rescaled (0.026 to 0.0064 per over-filled slot) so a stuffed bag tops out around the vanilla ~70% mobility loss instead of stacking past 100%
- Dropped-on-death bag enlarged to 13x11 (143) so a full 136-slot inventory actually fits in it

Pure XML modlet (XPath patches only), no DLLs.

**Game version:** 1.2.0 needs V3.3 or later. V3.3 rebuilt the backpack window around a scrolling grid, and the UI patch targets that layout. On V3.0 to V3.2, use 1.1.x.

## How the bag fits on screen

V3.3's backpack window is a scrollview holding an 8-wide grid (12 rows, 96 cells, in vanilla). The grid builds one item-stack controller per cell when the window opens for the first time, and a bag slot without a cell never renders, so the mod raises the grid to 17 rows: 8 x 17 = 136, one cell per slot. The window keeps its vanilla width and height and the extra rows scroll.

Up to 1.1.x the bag had to be on screen all at once, which made the window 1145px wide and needed a HUD size of 0.75 or lower. With the scrolling grid the backpack is vanilla width again, so that limit no longer applies.

## Install

Drop the `KitsuneBackpack` folder into your `Mods` folder. Needed on **both server and client**: bag data is pushed by the server, but the backpack grid is client-side UI, so players without the mod will not see their extra slots.

## Notes

- Growing the bag is safe on existing saves. Removing the mod later shrinks bags back to 45 and can orphan items in the removed slots.
- The same applies to shrinking it: going from 136 back to 72 orphans anything in slots 73-136.
- The loot window's item-stack controller pool is raised from 90 to 156 (`windowLooting` grid `cols` 9 to 13, `rows` 10 to 12). Vanilla builds that pool once and hides the spares, and per-container Columns/Rows are set at open time, so ordinary crates and safes are unchanged. 156 covers the 143-slot death bag and KitsuneStorage's 144-slot steel crate, since whichever of the two mods loads last sets this pool.
- The death bag is 13x11 rather than one long row. The loot window sits in the *left* stack panel next to the backpack in the *centre* one, and 7DTD packs those panels side by side, so every loot column costs 75px of screen width while V3.3's loot window scrolls vertically.
- Part of the Kitsune QoL family: [KitsuneMoreSloots](https://github.com/AdaInTheLab/KitsuneMoreSloots), [KitsuneStorage](https://github.com/AdaInTheLab/KitsuneStorage).
