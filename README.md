# svelt-rating-selector-display

This is a small svelt component that lets you easily get ratings/reviews from user and display them. It uses unicode characters and text as icons.

Features:

- Theming
- Custom Icons using unicode characters
- Get customer rating in whole numbers
- Display ratings with any amount of precision
- Set the number rating icons
- Keyboard shortcuts
- Handles Null values


## How to istall

```
npm i svelt-rating-selector-display
```


## How to use

### How to get ratings

```svelte
<script>
  import { RatingSelector } from 'svelte-rating-selector-display';
  let rating = Null; // This will be updated when a user selects a rating
</script>

<RatingSelector bind:rating enableSelection={true} />
```

### How to display ratings

```svelte
<script>
  import { RatingSelector } from 'svelte-rating-selector-display';
</script>

<RatingSelector rating={3.35} />
```

### Props

| Prop              | Type                           | Description                                                                      |
| :---------------- | :----------------------------- | :------------------------------------------------------------------------------- |
| `rating`          | number \| null                 | Inital displayed rating, if null no rating is displayed                          |
| `enableSelection` | boolean                        | If true the user can select a rating, if false a static rating will be displayed |
| `numberOfIcons`   | number                         | The number of icons to display for the rating                                    |
| `style`           | [key: string]: string; \| null | A list of styles to be applied to the parent element of the selector             |


## How to format

### CSS variables

Colors:

- `--icon-selected-color`
- `--icon-unselected-hover-color`
- `--icon-selected-hover-color`
- `--icon-unslected-color,`

Formating:

- `--icon-size`
- `--icon-spacing`
- `--selector-icon`

example:

```css
:root {
  --icon-selected-color: #211b27;
  --icon-unselected-hover-color: #948f97;
}
```

### Using style prop

```svelte
<script>
  import { RatingSelector } from 'svelte-rating-selector-display';
  const style = {
	'--icon-selected-color': '#211B27',
    '--icon-unselected-hover-color': '#948F97',
  };
</script>

<RatingSelector rating={3.7} {style} />
```
