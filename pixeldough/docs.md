# Pixeldough
By running a bit of code on each pixel in an image, you can make a lot of cool art!


## The API

```
// simply renders the image
forEachPixel(x, y) {
    return sample(x, y);
}
```


## (x, y)

(0, 0) is the top left

(1, 1) is the bottom right


## sample(x, y)

coordinates greater than 1 or less than 0 will "wrap around" such that (1.5, -0.2) is equivalent to (0.5, 0.2)


## red, green, blue, alpha

an image that is completely filled with the most intense red:
```
    return [1, 0, 0, 1];
```
the most intense green:
```
    return [0, 1, 0, 1];
```
the most intense blue:
```
    return [0, 0, 1, 1];
```

if the last coordinate is 0, your image will be completely transparent.

black is the absence of colors:
```
    return [0, 0, 0, 1];
```

white is the presence of all colors:
```
    return [1, 1, 1, 1];
```

## const [r, g, b, a] = sample(x, y)
sample returns an array of color values, just as your forEachPixel function does.


## just an image

<img width="300" src="https://cloud-i3n4o8a50-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(x, y);
      return [r, g, b, a];
    }
})
```

## flip!

<img width="300" src="https://cloud-dp3v55kn2-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(y, x);
      return [r, g, b, a];
    }
})
```

## darken

<img width="300" src="https://cloud-8jfg4stx4-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(x, y);
      return [r - 0.3, g - 0.3, b - 0.3, a];
    }
})
```

## invert

<img width="300" src="https://cloud-r7hx0ta6p-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(x, y);
      return [1 - r, 1 - g, 1 - b, a];
    }
})
```

## add to color based on position in image

<img width="300" src="https://cloud-mn6pntdgf-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(x, y);
      return [x+r, y+g, b, a];
    }
})
```

## mix two colors

<img width="300" src="https://cloud-nk2ylrl7u-hack-club-bot.vercel.app/0image.png"></img>

```
const INDIGO = [0.3, 0.0, 0.6, 1];
const PEACH  = [1.0, 0.5, 0.4, 1];

render({
    size: [300, 300],
    forEachPixel(x, y) {
      return mix(PEACH, INDIGO, 0.5)
    }
})
```

## mix two colors based on position in image

<img width="300" src="https://cloud-6n5g2cl1k-hack-club-bot.vercel.app/0image.png"></img>

```
const INDIGO = [0.3, 0.0, 0.6, 1];
const PEACH  = [1.0, 0.5, 0.4, 1];

render({
    size: [300, 300],
    forEachPixel(x, y) {
      return mix(PEACH, INDIGO, x)
    }
})
```

## mix in an image!

<img width="300" src="https://cloud-19sfbea6p-hack-club-bot.vercel.app/0image.png"></img>

```
const INDIGO = [0.3, 0.0, 0.6, 1];
const PEACH  = [1.0, 0.5, 0.4, 1];

render({
    size: [300, 300],
    forEachPixel(x, y) {
      return mix(sample(x, y), INDIGO, x)
    }
})
```

## image grid!

<img width="300" src="https://cloud-kcj294dr2-hack-club-bot.vercel.app/0image.png"></img>

can you change the size of the grid based on position in image?

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const [r, g, b, a] = sample(x * 2, y * 2);
      return [r, g, b, a];
    }
})
```

## becoming well rounded!

<img width="300" src="https://cloud-p91oye7o3-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const dist = distance([x, y], [0.5, 0.5]);
      if (dist > 0.5)
        return [0, 0, 0, 1];
      else
        return sample(x, y);
    }
})
```

## mixing based on distance from center

<img width="300" src="https://cloud-ramis7fu2-hack-club-bot.vercel.app/0image.png"></img>

```
const BLACK = [0, 0, 0, 1];
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const dist = distance([x, y], [0.5, 0.5]);
      return mix(sample(x, y), BLACK, dist);
    }
})
```

## waves of red!

<img width="300" src="https://cloud-isa96zqtv-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const r = x % (1/4) * 4;
      return [r, 0, 0, 1];
    }
})
```

## sampling waves!

<img width="300" src="https://cloud-h3mki7fm9-hack-club-bot.vercel.app/0image.png"></img>

can you make the waves go up and down as well?

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const r = x % (1/4) * 4;
      return mix(sample(x, y), [0, 0, 0, 1], r);
    }
})
```

## laser pulses!

<img width="300" src="https://cloud-isa96zqtv-hack-club-bot.vercel.app/1image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const r = Math.sin(x * Math.PI * 5);
      return [r, 0, 0, 1];
    }
})
```

## circular pulses!

<img width="300" src="https://cloud-h3mki7fm9-hack-club-bot.vercel.app/2image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const dist = distance([x, y], [0.5, 0.5]);
      const r = Math.sin(dist * Math.PI * 11);
      return [r, 0, 0, 1];
    }
})
```

## using a circular pulse to mix an image with a flipped version of itself

<img width="300" src="https://cloud-h3mki7fm9-hack-club-bot.vercel.app/1image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const dist = distance([x, y], [0.5, 0.5]);
      let r = Math.sin(dist * Math.PI * 11);

      /* mix takes values that go from 0 to 1,
         but Math.sin returns values from -1 to 1. */
      r = (r + 1.0) * 0.5;

      return mix(sample(y, x), sample(x, y), r)
    }
})
```

## diamonds (XOR fractal)

<img width="300" src="https://cloud-h3mki7fm9-hack-club-bot.vercel.app/3image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const rx = x * 64;
      const ry = y * 64;
      const r = (rx ^ ry) / 64;
      return [r, 0, 0, 1];
    }
})
```

## using diamonds to mix in an image

<img width="300" src="https://cloud-isa96zqtv-hack-club-bot.vercel.app/2image.png"></img>

```
const BLACK = [0, 0, 0, 1];
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const rx = x * 64;
      const ry = y * 64;
      const r = (rx ^ ry) / 64;
      return mix(BLACK, sample(x, y), r);
    }
})
```

## mix two colors based on the angle between a pixel and the center

<img width="300" src="https://cloud-108r5firz-hack-club-bot.vercel.app/0image.png"></img>

```
const INDIGO = [0.3, 0.0, 0.6, 1];
const PEACH  = [1.0, 0.5, 0.4, 1];

render({
    size: [300, 300],
    forEachPixel(x, y) {
      let r = angleBetween([x, y], [0.5, 0.5]);

      /* the angle will go from 0 to 360,
         mix wants it to be from 0 to 1 */
      r = r / 360;

      return mix(INDIGO, PEACH, r);
    }
})
```

## turn angles back into positions on the screen

<img width="300" src="https://cloud-108r5firz-hack-club-bot.vercel.app/1image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      const angle = angleBetween([x, y], [0.5, 0.5]);
      const [nx, ny] = angleToPos(angle);
      return sample(nx, ny);
    }
})
```

## change the angles before you turn them back into positions!

<img width="300" src="https://cloud-108r5firz-hack-club-bot.vercel.app/3image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      let angle = angleBetween([x, y], [0.5, 0.5]);

      /* x is between 0 and 1,
         so we'll rotate the furthermost pixels 100 degrees */
      angle += 100 * x;
      
      const [nx, ny] = angleToPos(angle);
      return sample(nx, ny);
    }
})
```

## change the angle based on its distance from the center!

<img width="300" src="https://cloud-108r5firz-hack-club-bot.vercel.app/2image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      let angle = angleBetween([x, y], [0.5, 0.5]);

      const dist = distance([x, y], [0.5, 0.5]);
      angle += 100 * dist;

      const [nx, ny] = angleToPos(angle);
      return sample(nx, ny);
    }
})
```

## look for a pixel the same distance from the center as this one, just with a different angle

<img width="300" src="https://cloud-qs97l0wq2-hack-club-bot.vercel.app/0image.png"></img>

```
render({
    size: [300, 300],
    forEachPixel(x, y) {
      let angle = angleBetween([x, y], [0.5, 0.5]);

      const dist = distance([x, y], [0.5, 0.5]);
      angle += 100 * dist;

      /* angles are only a direction to look in;
         angleToPos assumes you want a pixel 1 unit away.
         (1 unit is the size of the entire image)
      
         let's have it look however far away this pixel is instead */
      const [nx, ny] = angleToPos(angle);
      return sample(nx * dist, ny * dist);
    }
})
```


[GitHub of this document.](https://github.com/hackclub/microworld-templates/blob/main/turtle/turtle-template.md)
