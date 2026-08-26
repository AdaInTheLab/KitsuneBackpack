# KitsuneBackpack

A 136-slot backpack for 7 Days to Die V3.x that keeps the vanilla locked-slot progression instead of handing you everything at spawn.

- **Bag size:** 45 to 136 (17 columns x 8 rows)
- **27 slots free at spawn**, the rest show as locked spaces, just like vanilla
- **Pack Mule** unlocks ~22 slots per level: a full 136 at level 5 (pocket mods still work on top)
- God mode and steroids unlock the whole bag
- Encumbrance penalty rescaled (0.026 to 0.0064 per over-filled slot) so a stuffed bag tops out around the vanilla ~70% mobility loss instead of stacking past 100%
- Dropped-on-death bag enlarged to 17x8 so a full 136-slot inventory actually fits in it

Pure XML modlet (XPath patches only), no DLLs.

## Why it is wide instead of tall

136 has no sensible 9-wide factoring, and the backpack grid cannot page: `XUiC_Backpack` has no paging support at all, and any slot without a visible grid cell is simply unreachable. So every slot has to be on screen at once. 17x8 keeps the window the same height it was at 72 slots and grows it sideways to 1145px instead of stretching it to ~1019px tall, where it would fight the loot window for vertical space.

## Install

Drop the `KitsuneBackpack` folder into your `Mods` folder. Needed on **both server and client**: bag data is pushed by the server, but the backpack grid is client-side UI, so players without the mod will not see their extra slots.

## Notes

- Growing the bag is safe on existing saves. Removing the mod later shrinks bags back to 45 and can orphan items in the removed slots.
- The same applies to shrinking it: going from 136 back to 72 orphans anything in slots 73-136.
- The loot window's item-stack controller pool is raised from 90 to 170 (`windowLooting` grid `cols` 9 to 17). Vanilla builds that pool once and hides the spares, and per-container Columns/Rows are set at open time, so ordinary crates and safes are unchanged.
- Part of the Kitsune QoL family: [KitsuneMoreSloots](https://github.com/AdaInTheLab/KitsuneMoreSloots), [KitsuneStorage](https://github.com/AdaInTheLab/KitsuneStorage).
