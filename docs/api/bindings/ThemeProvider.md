# ThemeProvider

ThemeProvider passes a single theme object down to its children. It can be used multiple times to compose different themes for different parts of the component tree. It uses the [context](https://facebook.github.io/react/docs/context.html) feature to pass down the theme.
<br>
Nested themes automatically get combined if not explicitly prevented. This helps if you only want to change or add a single value without repeating the whole theming used before.
<br>
<br>
[FelaComponent](FelaComponent.md), [createComponent](createComponent.md) and [connect](connect.md) automatically receive the theme as well.

## Props

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| theme | *Object* | | An object containing any theming information |
| overwrite | *boolean?* | `false` | Replace any passed down theme instead of merging it |

## Imports
```javascript
import { ThemeProvider } from 'react-fela'
import { ThemeProvider } from 'preact-fela'
import { ThemeProvider } from 'inferno-fela'
```

## Example

```javascript
const text = ({ theme }) => ({
  backgroundColor: theme.bgColor,
  fontSize: theme.fontSize,
  color: theme.color
})

const Text = createComponent(text)

const Fragmet = () => (
  <ThemeProvider theme={{ color: 'red', fontSize: '15px' }}>
    <Text>I am red and 15px sized</Text>
    <ThemeProvider theme={{ color: 'blue' }}>
      <Text>I am blue and 15px sized</Text>
    </ThemeProvider>
    <ThemeProvider theme={{ bgColor: 'yellow' }}>
      <Text>I am red and 15px sized with a yellow background</Text>
    </ThemeProvider>
  </ThemeProvider>
)
```

#### Overwriting themes
The `overwrite` option help to prevent theme inheritance for nested ThemeProvider components.

```javascript
const text = ({ theme }) => ({
  fontSiz: theme.fontSize,
  color: theme.color || 'red'
})

const Text = createComponent(text)

const Fragment = () => (
  <ThemeProvider theme={{ color: 'blue', fontSize: 15 }}>
    <Text>I am blue and 15px sized</Text>
    <ThemeProvider overwrite theme={{ fontSize: 20 }}>
      <Text>I am red and 20px sized</Text>
    </ThemeProvider>
  </ThemeProvider>
)
```
