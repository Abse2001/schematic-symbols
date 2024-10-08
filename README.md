# schematic-symbols

[View Online](https://symbols.tscircuit.com/)

Schematic symbols for tscircuit

## Usage

```ts
import { getSvg, resize, symbols } from "@tscircuit/schematic-symbols"

console.log(symbols.resistor.primitives)
// [{ type: "path", d: "M0 0L1 0...", color: "primary" }, {type: "text", text: "{REF}", ... }]
console.log(symbols.resistor.size)
// { width: 1, height: 0.6 }

getSvg(resistor)
// <svg><path d="M0 0L1 0... ...</svg>

// You can easily resize symbols
console.log(resize(symbols.resistor, { width: 100 }).size)
// { width: 100, height: 60 }
```

## Adding New Symbols

Go into the `./symbols` directory to add new shapes. After adding a shape file, it will
automatically appear in the dev environment (`npm run dev`). Here's an example of a shape
file:

```ts
// boxresistor.ts
import { path, text, defineSymbol } from "drawing"

export const boxresistor = defineSymbol({
  primitives: [
    path({ points: [[0, 0] /* ... */, , [1, 0]], color: "primary" }),
    text("{REF}", { x: 0.5, y: 0.3, anchor: "middle_top" }),
  ],
  ports: [
    { x: 0, y: 0, labels: ["1", "-"] },
    { x: 1, y: 0, labels: ["2", "+"] },
  ],
  center: { x: 0.5, y: 0 },
  size: { width: 1, height: 0.6 },
})
```

### Primitives

Various primitive JSON elements are defined to represent components, each primitive has
a function you can use to quickly define it inside new symbol definitions.

| Primitive | Description                                                 |
| --------- | ----------------------------------------------------------- |
| `path`    | A set of lines `{ points: Array<[number, number]>, color }` |
| `text`    | Text `{ text, x, y, anchor }`                               |
| `circle`  | Circle `{ x, y, radius }`                                   |
| `box`     | Box `{ x, y, width, height, anchor }`                       |

### Colors

You can use the following color aliases to color your symbol:

- `primary`
- `secondary`
- `background`

### Guidelines

The symbols should all look correct next to eachother, since they're all used together
in the same schematic.

- The width of most standard passives is `1`
- The height of most standard passives is `0.6`

### Development

Software needed to edit this project:
- VS Code
- Inkscape

## References

- [MIT Schematic Symbols](https://github.com/sjgallagher2/SchematicSymbolsSVG)
- [affinity-circuit-symbols-asset](https://github.com/keikawa/affinity-circuit-symbols-asset/tree/main)
- [Inkscape Symbols](https://github.com/upb-lea/Inkscape_electric_Symbols?tab=readme-ov-file)
