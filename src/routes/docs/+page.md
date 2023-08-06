
# svelt-rating-selector-display

This small, dependency-free Svelte component enables effortless user rating input and display. It offers seamless customization with Unicode characters to suit individual preferences. Moreover, it boasts full reactivity to ensure a smooth and dynamic user experience. Has user accesability, and allows keyboard input.

Features:

- Custom Theming
- Custom Icons Using Unicode Characters
- Get customer Ratings
- Present Ratings with Utmost Precision
- Set the Number Rating Icons
- All Props are Reactive
- Keyboard Shortcuts
- Built in User Accesability
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

| Prop              | Type                          | Description                                                                      | Default Value |
| :---------------- | :---------------------------- | :------------------------------------------------------------------------------- | :------------ |
| `rating`          | number \| null                | Inital displayed rating, if null no rating is displayed                          | null          |
| `enableSelection` | boolean \| null               | If true the user can select a rating, if false a static rating will be displayed | false         |
| `numberOfIcons`   | number \| null                | The number of icons to display for the rating                                    | 5             |
| `style`           | [key: string]: string \| null | A list of styles to be applied to the parent element of the selector             | null          |

If null is passed in for a prop, it will be set as the default value.

## How to format

### CSS variables

| Colors:                         | Default Value                                                                   | Description                                                                                             |
| :------------------------------ | :------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ |
| `--icon-selected-color`         | ![#ffd700](https://via.placeholder.com/15/ffd700/000000?text=+) `#ffd700`       | Color of rating icons when they are selected                                                            |
| `--icon-unselected-hover-color` | ![#ccc](https://via.placeholder.com/15/ccc/000000?text=+) `#ccc`                | Color of rating icons when they are not selected                                                        |
| `--icon-selected-hover-color`   | ![#f9dd39](https://via.placeholder.com/15/f9dd39/000000?text=+) `#f9dd39`       | Color of rating icons when they are selcted and hovered over                                            |
| `--icon-unslected-color`        | ![#f9e053b1](https://via.placeholder.com/15/f9e053b1/000000?text=+) `#f9e053b1` | Color of rating icons when they are unslected and hovered over                                          |
| `--focused-stroke-color`        | ![#ffffff](https://via.placeholder.com/15/ffffff/000000?text=+) `#ffffff`       | Color of stroke around rating icon when it is focused. This is for keyboard use, and user accessibility |

| Formating:              | Default Value | Description                                                                                            |
| :---------------------- | :------------ | :----------------------------------------------------------------------------------------------------- |
| `--icon-size`           | `3.5rem`      | Size of the rating icons                                                                               |
| `--icon-spacing`        | `0rem`        | Space between rating icons                                                                             |
| `--selector-icon`       | `★`           | Icon to be desplayed                                                                                   |
| `--focused-stroke-size` | `3px`         | Size of stroke around rating icon when it is focused. This is for keyboard use, and user accessibility |

example:

```css
:root {
	--icon-selected-color: #211b27;
	--icon-unselected-hover-color: #948f97;
	--selector-icon: '☆';
}
```

### Using style prop

```svelte
<script>
	import { RatingSelector } from 'svelte-rating-selector-display';
	const style = {
		'--icon-selected-color': '#211B27',
		'--icon-unselected-color': '#948F97',
		'--selector-icon': JSON.stringify('☆'), // Note: --selection-icon must be stringified
	};
</script>

<RatingSelector rating={3.7} {style} />
```
