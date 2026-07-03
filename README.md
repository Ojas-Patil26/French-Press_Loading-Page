# French Press — CSS Loading Screen

**[Live demo →](https://french-press-loading-page.vercel.app)**

A French press loading animation built with pure CSS keyframes and a small amount of vanilla JavaScript. The press brews and plunges while the page "loads", then pours itself out, drops a final drip, and bursts into a confetti splatter before fading away to reveal the page.

## How the loading screen works

The animation runs in five phases on a fixed timeline:

### 1. Brewing (0 – 1.5s)

![Brewing](screenshots/01-brewing.png)

On page load, dark coffee fills the carafe from the top (`fill-and-push` keyframes scale the `.dark-coffee` layer from `scaleY(0)` to full height) while the plunger sits raised above the lid.

### 2. Plunging (1.5 – 3s)

![Plunging](screenshots/02-plunging.png)

The plunger descends (`plunge` keyframes), pressing the dark grounds to the bottom of the carafe. As it plunges, the lighter `.brewed-coffee` layer is revealed above the filter (`reveal-brewed`). The plunger reaches the bottom at exactly 3s.

### 3. Pouring (3 – 4.95s)

![Pouring](screenshots/03-pouring.png)

At the 3s mark, JavaScript adds the `is-loaded` class to the wrapper. This triggers `pour-once`, rotating the whole press 90°. The coffee inside counter-rotates by −90° (`fluid-pour`) so it stays level with gravity, then slides out of the carafe (`translateX(-100%)`) as if being poured.

### 4. The final drop (4.95 – 5.75s)

![Drop](screenshots/04-drop.png)

A single drop pops out of the spout with a bouncy overshoot easing (`cubic-bezier(0.34, 1.56, 0.64, 1)`), then accelerates under "gravity" (`cubic-bezier(0.5, 0, 1, 1)`) until it hits the bottom of the screen.

### 5. Splatter and fade-out (5.75s – 7.75s)

![Splatter](screenshots/05-splatter.png)

The moment the drop lands (2750ms after `is-loaded`), `createSplatter()` spawns 80 dash-shaped particles at the impact point. Each gets a random color, size, angle, and velocity via CSS custom properties (`--tx`, `--ty`, `--rot`), and flies outward over 3s while fading. Simultaneously, the black wrapper fades out over 2s to reveal the page underneath.

![Fade out](screenshots/06-fadeout.png)

## Timing reference

| Time | Event |
|------|-------|
| 0ms | Coffee fills carafe |
| ~1500ms | Plunger starts descending |
| 3000ms | `is-loaded` added; press rotates 90° |
| 4950ms | Drop leaves the spout |
| 5750ms | Drop lands; splatter fires; fade-out begins |
| 7750ms | Loading screen fully transparent |

## Getting started

```bash
npm install
npm run dev
```

## License

[MIT](LICENSE)
