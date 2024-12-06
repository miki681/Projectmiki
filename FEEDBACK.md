## Picture aspect ratio

The people in the Culture and Heritage picture look squashed. This is because the original photo has dimensions of 1200 x 800 px, which is a 3:2 aspect ratio.

Your CSS for these images is:
```css
.card img {
  width: 500px;
  height: 450px;
}
```

500 x 450 px is a 10:9 aspect ratio (or 3:2.7).

To make the people look more natural, you can use the `object-fit` property, to tell the browser to fill the available area and clip any excess width or height:

```css
.card img {
  width: 500px;
  height: 450px;
  object-fit: cover;
}
```

However, your Riviera picture is 640 x 426 px and your `Mountains` picture is 900 x 598 px. All the pictures aspect ratios are very close to 3:2. Perhaps a better solution would be to use a 3:2 aspect ratio for `.card img`, so that the images are neither squashed nor (strongly) clipped:

```css
.card img {
  width: 510px;
  height: 340px;
  object-fit: cover;
}
```

Another alternative would be to set only the height of the images. In this case, their widths will adjust automatically, to maintain their original aspect ratio.

```css
.card img {
  /* width: auto; */
  height: 340px;
}
```

However, if you (or a colleague) later decides to use a picture whose aspect ratio is very different from 3:2, then the effect might not be what you want.

For my version of your site, I've chosen a slightly different approach, which assumes that all the images will have the same aspect ratio:
```css
.card img {
  width: 510px;
  max-width: 100vw;
}
```
This ensures that at widths of < 500px, the images will become smaller to fit the space available.

## Typo

"Heritage" has only one "r"

## Responsivity

Your site looks good in a wide viewport, like on a desktop, and also in a narrow viewport, like in portrait mode on a smartphone. But in between these two extremes, it might look a little strange. At 768px, it toggles between these two states:

![Narrow](images/narrower.webp)

At less than 768px, the images do not fill the frame around them.

![Wider](images/wider.webp)

Between 768px and about 1600px, the images appear in a horizontal line which is wider than the page.

You can fix all these issues and remove the need for any @media queries by using `flex-wrap: wrap` for your `.grid` element:

```css
 .grid {
   display: flex;
   flex-wrap: wrap;
   gap: 20px;
 }
 ```

 However, this will force your `.grid` to fit inside its parent `section`, for which you have set `max-width: 1200px`. If you comment out this setting, then your page behaves nicely at all widths.

 ```css
 section {
  padding: 50px 20px;
  /* max-width: 1200px; */
  margin: auto;
}
```