# PaletLab · Skladište Sisak — 3D warehouse loop

A single-file Three.js web app (`index.html`) that plays a 10-second looping 3D
animation of a busy pallet warehouse on the edge of Sisak, framed for a vertical
9:16 (1080×1920) video.

**Live:** https://klindic.github.io/pallet-warehouse-loop/

## What's in it

- Three.js r170 from jsDelivr via an import map. Every block is a `RoundedBoxGeometry`
  with `MeshStandardMaterial`. One sun with soft, light PCF shadows plus a hemisphere light,
  ACES tone mapping and a GTAO ambient-occlusion pass. No image textures and no 3D text.
- High-key "toy diorama" look: a white world with chunky rounded models, royal/navy blue
  accents, solar panels on the hall roof, lollipop trees, red-roof houses and bobbing
  map pins. Animation only; there is no on-screen UI.
- The diorama builds itself in the first second: slab, hall, racks, pallets level by
  level, then trees, houses and vehicles pop in.
- After that a 10 s action cycle loops seamlessly:
  - The bay truck opens its curtain. The forklift takes a pallet off the trailer,
    drives through the door and down the aisle, lifts and slides it into a rack slot.
  - A reach stacker picks the outbound pallet from that slot and loads it onto the
    same truck, which then closes its curtain and leaves through the west exit.
  - The waiting truck rolls from P2 onto the bay. Meanwhile a new truck enters through
    the east gate and parks in P2.
  - Cars pass on the street, the gate barriers lift, flags wave and the beacon turns.
- Five identical fleet trucks run one 50 s circuit, spaced 10 s apart. That way every
  truck, the forklift and every pallet are back in their starting positions at t = 10 s.

## URL parameters

| Param | Effect |
| --- | --- |
| `?build=0` | skip the 1 s build-in and start straight in the loop |
| `?t=4.2` | freeze at a given cycle time (seconds) |
| `?q=0.5` | render-resolution factor (lower = faster) |
| `?ao=0` | disable the GTAO pass |
| `?pins=0` | hide the floating map pins |
| `?manual` | don't auto-play; drive frames with `window.__wh.renderAt(T)` |

## Recording the loop

Open the page in a 1080×1920 viewport, for example with Chrome DevTools device mode
or a headless browser. The stage fills that frame exactly; other window sizes are
letterboxed to 9:16. The 10 s loop runs from T = 1 s to T = 11 s and repeats from
there. For frame-exact export use `?manual` and call `window.__wh.renderAt(1 + n / fps)`
for each frame.
