# KitsuneBackpack

Bigger backpacks for 7 Days to Die V3.3 that keep the vanilla locked-slot progression instead of handing you everything at spawn. Two mods live in this repo. **Install one, not both:**

| | **KitsuneBackpack** (136) | **KitsuneBackpack200** (200) |
|---|---|---|
| Bag size | 136, fixed | 104, up to 200 with a Q6 Large backpack |
| Vanilla backpack items | no effect (the bag is already full size) | doubled: Small +4 to +32, Medium +36 to +64, Large +68 to +96 |
| Free at spawn | 32 | 32 |
| Pack Mule | ~21 per level, all 136 at level 5 | 12/36/72/120/168, all 200 at level 5 |
| Death bag | 8x20 (160) | 8x28 (224) |
| Encumbrance per over-filled slot | 0.0067 | 0.0042 |

Both:

- Free slots are vanilla's 32 base carry (scaled by the sandbox carry setting). The rest show as locked spaces until Pack Mule or pocket mods unlock them.
- God mode and steroids unlock the whole bag, as they do in vanilla. On V3.4 so do Chicken Nuggets, the Twitch Pack Mule buff, the complete Fireman's Almanac (in biomes 8 and 9) and the Night Stalker thief book at night, which V3.4 made whole-bag effects.
- Encumbrance is rescaled so a stuffed bag tops out around vanilla's ~70% mobility loss instead of stacking past 100%.
- Pure XML modlets (XPath patches only), no DLLs.

**Game version:** V3.3 or later, tested on V3.3 and V3.4. V3.3 rebuilt the backpack window around a scrolling grid and added a bag size cap, and both mods target that. On V3.0 to V3.2, use KitsuneBackpack 1.0.1.

## How the bag fits on screen

V3.3's backpack window is a scrollview holding an 8-wide grid (12 rows, 96 cells, in vanilla). The grid builds one item-stack controller per cell when the window opens for the first time, and a bag slot without a cell never renders, so the mods raise the grid to one cell per slot: 8 x 17 = 136, or 8 x 25 = 200. The window keeps its vanilla width and height and the extra rows scroll.

## Install

Drop **one** of the `KitsuneBackpack` or `KitsuneBackpack200` folders into your `Mods` folder.

- **Dedicated server:** install it on the **server only**. Both mods are pure XML, and a dedicated server sends its patched XML to every client that joins, the backpack grid (`XUi_InGame`) included, so players need nothing and can keep EAC on. Installing it on clients as well does no harm.
- **Single player or a game you host:** install it on your own machine, since you are the server.

With KitsuneStorage, use KitsuneStorage 1.0.3 or later alongside KitsuneBackpack200. Older versions shrink the loot window pool back to 192, and the bottom of a full 200 death bag won't show.

## Notes

- **V3.4.** V3.4 raised four carry effects to 96, vanilla's whole bag: Chicken Nuggets (was 48), the Twitch Pack Mule buff (50), the complete Fireman's Almanac in biomes 8 and 9 (45) and the Night Stalker thief book (27). 1.2.3 raises them to the whole bag here (136 or 200), on V3.4 only: V3.3 keeps its own values. V3.4's vanilla backpack grid also has 24 rows (192 cells) with only 96 used; the mods' 17 and 25 rows still give exactly one cell per slot.
- **The bag size cap.** V3.3 added `MaxBagSize` (96) to the player and clamps the bag to it, so both mods raise it. KitsuneBackpack 1.2.0 missed this and stayed at 96 on V3.3. 1.2.1 fixes that.
- **The death bag holds more than the bag.** With drop-on-death set to everything, the game puts the bag, the toolbelt (10) and the equipment (up to 13) into a single dropped bag, and anything that doesn't fit is lost. That's why the death bags are 160 and 224, not 136 and 200. They stay 8 wide like vanilla: V3.3's loot window is as wide as the container's columns and scrolls vertically, so extra rows cost nothing next to the backpack.
- **The loot window pool.** The loot window builds its pool of item-stack controllers once, from its grid's rows x cols (90 in vanilla), and never shows slots past it. KitsuneBackpack needs 168, KitsuneBackpack200 228, and KitsuneStorage 192 for its 144-slot steel crate. All three use 12 columns and only ever raise the rows, so whichever loads last can't shrink the pool below what another needs. Per-container Columns/Rows are set at open time, so ordinary crates and safes are unchanged.
- Growing the bag is safe on existing saves. Removing the mod later shrinks bags back to vanilla and can orphan items in the removed slots. The same goes for switching from KitsuneBackpack200 to KitsuneBackpack with more than 136 slots in use.
- Part of the Kitsune QoL family: [KitsuneMoreSloots](https://github.com/AdaInTheLab/KitsuneMoreSloots), [KitsuneStorage](https://github.com/AdaInTheLab/KitsuneStorage).

## License

[CC BY-NC-SA 4.0](LICENSE), with an extra permission for servers that make money: see [NOTICE.md](NOTICE.md). In short: play it, change it and share it, with credit, not for sale, and with changed versions under the same license.
