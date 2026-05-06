[← Docs](../README.md)

# Using an icon pack

*How-to guide.*

This page covers what's the same for every Ichava icon pack: install, render, fluent helper, browser preview. Pack-specific knobs (stroke width, variant defaults, brand attribution) live in each pack's own `docs/` directory.

## 1. Install a pack

Pick one (or several) and require it alongside `ichava/core`.

```bash
composer require ichava/core ichava/tabler-icons
```

The pack's service provider registers automatically via Laravel package discovery. No manual `config/app.php` edit.

## 2. Render an icon in a Blade view

The generic component works with any installed pack:

```blade
<x-ichava::icon name="ichava/tabler-icons::home" class="w-6 h-6" />
```

The `name` follows the [icon path format](../core/icon-path-format.md): `vendor/package::category/icon`.

## 3. Render with the global helper

```blade
{{ ichava('ichava/tabler-icons::home')->color('#4338ca')->class('w-6 h-6') }}
```

See [global helper](../core/global-helper.md) for the full fluent API.

## 4. Search visually with `ichava/browser`

If you also have `ichava/browser` installed, the visual browser renders every icon from every installed pack:

```
http://example.com/ichava/icons
```

Filter by pack, by variant or category, by name. Copy the path with one click.

## 5. Seed pack icons into the database

Optional, but recommended for production. Seeding builds a fast lookup index used by the search API and the Blade renderer.

```bash
php artisan ichava:database seed --package=ichava/tabler-icons
```

See [seeding pack icons](seeding-pack-icons.md).

## Where to find pack-specific docs

Each pack's repository has a `docs/` directory:

- [`ichava/tabler-icons/docs/`](https://github.com/ichava/tabler-icons/tree/main/docs)
- [`ichava/bundled-icons/docs/`](https://github.com/ichava/bundled-icons/tree/main/docs)
- [`ichava/metronic-icons/docs/`](https://github.com/ichava/metronic-icons/tree/main/docs)

Look there for stroke widths, variant lists, attribution, and any pack-specific behaviour.

## See also

- [Icon path format](../core/icon-path-format.md)
- [Blade components](../core/blade-components.md)
- [Global helper](../core/global-helper.md)
- [Seeding pack icons](seeding-pack-icons.md)
- [Building your own pack](building-your-own.md)
