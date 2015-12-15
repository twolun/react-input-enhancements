# react-input-enhancements
Set of enhancements for input control

The intention of creating this library was to bring `input` component out of the dropdown/autocomplete/whatever code, so it could be easily replaced with your custom component, and also to split independent functionality into different components, which could be combined with each other (still not quite sure it was worth it, though).

There are currently four components:

1. [`<Autosize />`](#Autosize)
2. [`<Autocomplete />`](#)
3. `<Dropdown />`
4. `<Mask />`

All components accept `function` as a child, providing props as a first argument, which you should pass to your `input` component. If there is nothing else except `input`, it could be passed as a child directly (for simplicity).

[`<Combobox />`](#Combobox) is a combination of `Dropdown`, `Autosize` and/or `Autocomplete` components.

## Autosize

`Autosize` resizes component to fit it's content.

```js
<Autosize defaultValue={value}
          minWidth={100}>
  {(inputProps, { width }) =>
    <input type='text' {...inputProps} />
  }
</Autosize>
```

### Autosize Props

* **`value`** *string* - Input value (for a controlled component)
* **`defaultValue`** *string* - Initial value (for a uncontrolled component)
* **`getInputElement`** *function()* - Optional callback that provides input DOM element
* **`defaultWidth`** *number* - Minimum input width

## Autocomplete

`Autocomplete` prompts a value based on provided `options` (see also [react-autocomplete](https://github.com/rackt/react-autocomplete) for the same behaviour)

```js
<Autocomplete defaultValue={value}
              options={options}>
  {(inputProps, { matchingText, value }) =>
    <input type='text' {...inputProps} />
  }
</Autocomplete>
```

### Autocomplete Props

* **`value`** *string* - Input value (for a controlled component)
* **`defaultValue`** *string* - Initial value (for a uncontrolled component)
* **`getInputElement`** *function* - Optional callback that provides input DOM element
* **`options`** *array* - Array of options that are used to predict a value

`options` is an array of strings or objects with a `text` or `value` string properties.

## Dropdown

`Dropdown` shows a dropdown with a (optionally filtered) list of suitable options.

```js
<Dropdown defaultValue={value}
          options={options}>
  {(inputProps, { textValue }) =>
    <input type='text' {...inputProps} />
  }
</Dropdown>
```

### Dropdown Props

* **`value`** *string* - Input value (for a controlled component)
* **`defaultValue`** *string* - Initial value (for a uncontrolled component)
* **`options`** *array* - Array of shown options
* **`onRenderOption`** *function(className, style, option)* - Renders option in list
* **`onRenderCaret`** *function(className, style, isActive, children)* - Renders a caret
* **`onRenderList`** *function(className, style, isActive, listShown, children, header)* - Renders list of options
* **`onRenderListHeader`** *function(allCount, shownCount, staticCount)* - Renders list header
* **`dropdownClassName`** *string* - Dropdown root element class name
* **`dropdownProps`** *object* - Custom props passed to dropdown root element
* **`optionFilters`** *array* - List of option filters

`options` is an array of strings or objects with a shape:

* **`value`** - "real" value of on option
* **`text`** - text used as input value when option is selected
* **`label`** - text or component rendered in list
* **`static`** - option is never filtered out or sorted
* **`disable`** - option is not selectable

`null` option is rendered as a separator

`optionFilters` is an array of filters for options (for convenience). By default, these filters are used:

* `filters.filterByMatchingTextWithThreshold(20)` - filters options by matching value, if options length is more than 20
* `filters.sortByMatchingText` - sorting by matching value
* `filters.limitBy(100)` - cuts options longer than 100
* `filters.notFoundMessage('No matches found')` - shows option with 'No matches found' label if all options are filtered out
* `filters.filterRedudantSeparators` - removes redudant separators (duplicated or at the begin/end of the list)

## Mask

`Mask` formats input value.

```js
<Mask defaultValue={value}
      pattern='0000-0000-0000-0000'>
  {(inputProps, { value }) =>
    <input type='text' {...inputProps} />
  }
</Mask>
```

### Mask Props

* **`value`** *string* - Input value (for a controlled component)
* **`defaultValue`** *string* - Initial value (for a uncontrolled component)
* **`getInputElement`** *function()* - Optional callback that provides input DOM element
* **`pattern`** *string* - Pattern for formating string. Only '0' (digit) or 'a' (letter) pattern chars are currently supported.
* **`emptyChar`** *string* - Character used as an empty symbol (`' '` by default)
* **`onUnmaskedValueChange`** *function(text)* - Fires when value is changed, providing unmasked value

## Some other (probably better) implementations

* [react-autocomplete](https://github.com/rackt/react-autocomplete) - Dropdown with autocompletion by Ryan Florence (that led me to create this library)
* [react-maskedinput](https://github.com/insin/react-maskedinput) - More advanced masked input by Jonny Buchanan
