# Button Class

This section covers the PowerGrid Buttons Class.

Here you will find:

[[toc]]

## Introduction

PowerGrid offers a convenient way to display buttons in your [Table Rows](/table-features/rows.html#buttons) and a Header button for [Bulk Actions](/table-features/bulk-actions.html).

Please, refer to the sections linked above to see how to use buttons in each case. Below, we will explore the configuration methods for the `Button::class`.

## Usage

See [Table Rows](/table-features/rows.html#buttons) and  [Bulk Actions](/table-features/bulk-actions.html).

## Button Methods

The methods below can be chained to the `PowerComponents\LivewirePowerGrid\Button` class.

### add()

Creates a new button.

| Parameter        | Description                  |
|------------------|------------------------------|
| (string) $action | internal name of this button |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('create-dish'),
```

---

### slot()

Render the given HTML.

| Parameter         | Description |
|-------------------|-------------|
| (string) $slot    | HTML string |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('create-dish')  
        ->slot("&#9889; Edit"),
```

---

### class()

Sets the button's CSS class attribute.

| Parameter           | Description      |
|---------------------|------------------|
| (string) $classAttr | CSS class        |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('create-dish')  
    ->slot('Create a dish')
    ->class('bg-indigo-500 text-white'),
```

---

### dispatch()

Dispatch events.

| Parameter                | Description   |
|--------------------------|---------------|
| (string) $event          | Name of event |
| (array, Closure) $params | Parameters    |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('create-dish')  
    ->slot('Create a dish')
    ->class('bg-indigo-500 text-white')
    ->dispatch('postAdded', ['key' => $row->id]),
```

The code above is equivalent to:

```html{2}
<div>
    <button wire:click="$dispatch('postAdded', { key: 1})">
</div>
```

::: tip 💡 TIP
Read more about [Events](https://livewire.laravel.com/docs/events###dispatching-events) in the Livewire documentation.
:::

---

### dispatchTo()

Dispatch Events to a target.

| Parameter                | Description    |
|--------------------------|----------------|
| (string) $to             | Component name |
| (string) $event          | Name of event  |
| (array, Closure) $params | Parameters     |

The code below:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->dispatchTo('admin-component', 'postAdded', ['key' => $row->id]),
```

is equivalent to:

```html{2}
<div>
    <button wire:click="$dispatchTo('admin-component', 'postAdded', { key: 1})">
</div>
```

::: tip 💡 TIP
Read more about [Events](https://livewire.laravel.com/docs/events###dispatching-events) in the Livewire documentation.
:::

---

### openModal()

Opens a modal window using [wire-elements/modal](https://github.com/wire-elements/modal) package. You must install Wire Elements to use this functionality.

| Parameter                | Description                                           |
|--------------------------|-------------------------------------------------------|
| (string) $component      | You must pass the `View` of Livewire Modal component. |
| (array, Closure) $params | This is the component parameter.                      |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->openModal('view-dish', ['dish' => 'id']),
```

---

### method()

Sets the Action HTTP method.

| Parameter        | Description                                |
|------------------|--------------------------------------------|
| (string) $method | Valid methods: `get`/`post`/`put`/`delete` |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->method('delete'),
```

---

### route()

Sets the Action route.

| Parameter       | Description         |
|-----------------|---------------------|
| (string) $route | Valid Laravel route |
| (array) $params | Route parameters    |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->route('dish.edit', ['dish' => $row->id]),
```

---

### target()

Sets the target for the specified route.

| Parameter        | Default          | Default |
|------------------|------------------|---------|
| (string) $target | HTML href target | _blank  |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->target('_self'),
```

---

### can()

Checks if the button has permission to be rendered.

| Parameter     | Default                                         | Default |
|---------------|-------------------------------------------------|---------|
| (string) $allowed | If `false`, the button will not be rendered. | true    |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('edit-dish')
    ->slot('Edit')
    ->route('dish.edit', ['dish' => $row->id])
    ->can(allowed: auth()->check()),
```

---

### tooltip()

Sets the button's tooltip (title attribute).

| Parameter         |
|-------------------|
| (string) $tooltip |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('edit-dish')
    ->slot('Edit')
    ->route('dish.edit', ['dish' => $row->id])
    ->tooltip('Edit Record'),
```

---

### toggleDetail()

Toggle (expand/collapse) the [Detail Row](/table-component/component-configuration.html#detail-row).

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('toggle-detail')
    ->slot('Toggle Detail')
    ->toggleDetail(),
```

### bladeComponent()

Allows you to add a custom component overriding all default behavior

| Parameter           | Default                     |
|---------------------|-----------------------------|
| (string) $component | View component path (blade) |
| (array) $params     | Blade parameters            |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('my-custom-button')
    ->bladeComponent('my-custom-button', ['dishId' => $row->id]),
```

---

### render()

Renders HTML.

| Parameter          | Default         |
|--------------------|-----------------|
| (Closure) $closure | Closure (Model) |

Example:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('custom')
     ->render(function ($dish) {
        return Blade::render(<<<HTML
<x-button.circle primary icon="pencil" wire:click="editStock('$dish->id')" />
HTML);
}),     
```

---

### id()

 Add custom html id attribute.

| Parameter       |
|-----------------|
| (string) $value |

The code below:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('view')
    ->slot('View')
    ->class('btn btn-primary')
    ->id('view'), 
```

is equivalent to:

```html
<button id="view-1"> // 1 - is the value set in the current row using primaryKey = id.
```

## Conditional Formatting

See [Conditional Rules](/table-features/conditional-rules.html).

## Extending the Button::class

You can extend the `Button::class` via Laravel's [Macroable](https://laravel.com/api/11.x/Illuminate/Support/Traits/Macroable.html) feature.

The class a has built-in `dynamicProperties` variable which can be used to store custom method parameters.

The following code adds a custom `icon()` method to the `Button` class.

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::macro('icon', function (string $name) {
    $this->dynamicProperties['icon'] = $name;

    return $this;
});
```

As a result, the method can now be chained to the class as demonstrated below:

```php
use PowerComponents\LivewirePowerGrid\Button;

Button::add('new-modal')
    ->slot('New window')
    ->class('bg-gray-300')
    ->icon('fa-window')
    ->openModal('new', []),
```
