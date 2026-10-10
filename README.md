# KitsuneBackpack

A 136-slot backpack for 7 Days to Die V3.x that keeps the vanilla locked-slot progression instead of handing you everything at spawn.

- **Bag size:** 45 to 136 (17 columns x 8 rows)
- **27 slots free at spawn**, the rest show as locked spaces, just like vanilla
- **Pack Mule** unlocks ~22 slots per level: a full 136 at level 5 (pocket mods still work on top)
- God mode and steroids unlock the whole bag
- Encumbrance penalty rescaled (0.026 to 0.0064 per over-filled slot) so a stuffed bag tops out around the vanilla ~70% mobility loss instead of stacking past 100%
- Dropped-on-death bag enlarged to 13x11 (143) so a full 136-slot inventory actually fits in it

Pure XML modlet (XPath patches only), no DLLs.

## Why it is wide instead of tall

136 has no sensible 9-wide factoring, and the backpack grid cannot page: `XUiC_Backpack` has no paging support at all, and any slot without a visible grid cell is simply unreachable. So every slot has to be on screen at once. 17x8 keeps the window the same height it was at 72 slots and grows it sideways to 1145px instead of stretching it to ~1019px tall, where it would fight the loot window for vertical space.

## Install

Drop the `KitsuneBackpack` folder into your `Mods` folder. Needed on **both server and client**: bag data is pushed by the server, but the backpack grid is client-side UI, so players without the mod will not see their extra slots.

### Set HUD size to 0.75 or lower

A 1145px-wide backpack does not fit every HUD size. 7DTD lays its menus out as three stack panels packed side by side (left / centre / right) and centres the row on screen, with no clamping: whatever does not fit runs off both edges. The usable width scales as 1/HUD-size, so it is roughly 1750 units at 1.0 and 2500 at 0.70, and this bag pushes the centre panel from 606 to 1145.

Measured against that budget (units, after the 1.05 stack scale):

| Screen | Needs | Max HUD size |
|---|---|---|
| Backpack on its own | 1202 | 1.0 |
| Workbench / forge | 1877 | 0.93 |
| Character | 1900 | 0.92 |
| Looting an ordinary crate | 1920 | 0.91 |
| Looting your own death bag | 2235 | 0.78 |

**0.75 covers everything with room to spare.** Above ~0.78 the death bag starts running off the edges, and above ~0.91 so does everything else. Nothing overlaps at any setting, it just gets clipped by the screen. Ultrawide gets more width and can go higher.

## Notes

- Growing the bag is safe on existing saves. Removing the mod later shrinks bags back to 45 and can orphan items in the removed slots.
- The same applies to shrinking it: going from 136 back to 72 orphans anything in slots 73-136.
- The loot window's item-stack controller pool is raised from 90 to 143 (`windowLooting` grid `cols` 9 to 13, `rows` 10 to 11). Vanilla builds that pool once and hides the spares, and per-container Columns/Rows are set at open time, so ordinary crates and safes are unchanged.
- The death bag is 13 wide, not 17, even though the backpack is 17. The loot window sits in the *left* stack panel and the backpack in the *centre* one, and 7DTD packs those panels side by side rather than overlapping them, so a 17-wide death bag put ~1275px of loot window next to a 1145px backpack. 13x11 trades height, which the left panel has spare, for 300px of width it does not. It stops at 11 rows because the loot grid grows downward from a fixed top: vanilla's deepest container is 10 rows and already lands close to the toolbelt, so 11 is one row past anything the game itself ships and 12 was pushing it.
- Part of the Kitsune QoL family: [KitsuneMoreSloots](https://github.com/AdaInTheLab/KitsuneMoreSloots), [KitsuneStorage](https://github.com/AdaInTheLab/KitsuneStorage).
