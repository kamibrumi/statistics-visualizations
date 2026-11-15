# How much can you trust an average?

An interactive, scroll-driven explainer of the **standard error**, written for students new to statistics.

**▶ Live:** https://kamibrumi.github.io/statistics-visualizations/standard-error-viz/

The story follows a coffee shop that wants to know how long customers wait for their order. It starts with a single sample and builds up to the sampling distribution of the mean. Along the way it shows why the standard error is what tells you how far to trust one sample's average.

## The story

The page is split in two: the story scrolls on the left, and a chart stays fixed on the right and updates at each step.

| Act | What the reader learns |
|---|---|
| **1. One sample** | What a sample is, what **n** is (each dot is one customer), and the sample mean **x̄** as a guess for the true average **μ** |
| **2. Why one mean isn't enough** | A second sample gives a different x̄: the sample mean is itself random |
| **3. The distribution of the sample means** | 20 samples, each mean dropping into a histogram: the **sampling distribution of the sample mean**, centered on μ |
| **4. The standard error** | The spread of those means is the **standard error (SE)**. It's compared with the spread of individual waits (**σ**) and with the shortcut **SE = σ/√n**. More samples give a *more precise measurement* of the SE without changing it; a bigger **n** makes the SE smaller (4× the customers halves it). |
| **5. Back to the real world** | With only one sample, x̄ usually lands within about 1 SE of μ, and almost never more than 2–3 SE away |
| **Your turn** | A sandbox: change the number of samples and n, sort the samples by x̄, or draw new samples |

Key terms are color-coded the same way in the text and the chart: **μ** red, **x̄** teal, **SE** amber, **σ** magenta, **σ/√n** blue.

## Run it locally

It's a single, self-contained `index.html` with no build step. Serve the folder with any static web server, for example:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/standard-error-viz/ in your browser.

Opening the file directly (`file://`) may also work, but a local server behaves the same as the live site.

## How it's built

- **Plain HTML, CSS and JavaScript**: no framework, and charts are drawn as SVG.
- **[Scrollama](https://github.com/russellsamora/scrollama) 3.2.0**, loaded from the jsDelivr CDN, triggers each step as it scrolls into view. If it can't load, a built-in `IntersectionObserver` fallback takes over.
- **Simulated data.** A hidden population of 10,000 wait times (μ = 5 min, σ = 1 min) is generated with a seeded random number generator, so the numbers in the story are the same on every visit. Each sample has its own random stream, so adding samples keeps the existing ones, and raising n adds customers to every sample.
- **The numbers in the text are computed from the data**, so the story and the chart always agree.
- Light and dark mode follow your system setting. Animations are skipped if your system asks for reduced motion.

### Where to change things (in `index.html`)

| What | Look for |
|---|---|
| The story text | the `<section class="step">` blocks |
| What the chart shows at each step | the `STEPS` array (one entry per step, in the same order) |
| The population (mean, spread, size) | `const N = 10000, MU = 5, SIGMA = 1` |
| Which samples are drawn | `BASE_SEED` |
| Sandbox limits for samples and n | `LIMITS` |
| Chart axis ranges | `RANGE` |
| Colors | the CSS variables at the top of the `<style>` block |

## Contributing

Ideas, corrections and improvements are welcome. Please open an issue or a pull request on [kamibrumi/statistics-visualizations](https://github.com/kamibrumi/statistics-visualizations).

## Credits

Designed by [Camelia D. Brumar](https://kamibrumi.github.io/).
