# KitsuneBackpack

A 72-slot backpack for 7 Days to Die V2.x that keeps the vanilla locked-slot progression instead of handing you everything at spawn.

- **Bag size:** 45 to 72 (8 rows of 9)
- **27 slots free at spawn**, the rest show as locked spaces, just like vanilla
- **Pack Mule** unlocks 9 slots per level: a full 72 at level 5 (pocket mods still work on top)
- God mode and steroids unlock the whole bag
- Encumbrance penalty rescaled (0.026 to 0.015 per over-filled slot) so a stuffed bag tops out around the vanilla ~70% mobility loss instead of stacking past 100%
- Dropped-on-death bag enlarged to 9x8 so a full 72-slot inventory actually fits in it

Pure XML modlet (XPath patches only), no DLLs.

## Install

Drop the `KitsuneBackpack` folder into your `Mods` folder. Needed on **both server and client**: bag data is pushed by the server, but the backpack grid is client-side UI, so players without the mod will not see their extra slots.

## Notes

- Growing the bag is safe on existing saves. Removing the mod later shrinks bags back to 45 and can orphan items in the removed slots.
- Part of the Kitsune QoL family: [KitsuneMoreSloots](https://github.com/AdaInTheLab/KitsuneMoreSloots), [KitsuneStorage](https://github.com/AdaInTheLab/KitsuneStorage).
