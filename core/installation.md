[← Docs](../README.md)

# Installation

*How-to guide.*

## 1. Require the package

```bash
composer require ichava/core
```

The `IchavaServiceProvider` registers automatically via Laravel package discovery.

## 2. Publish the config

```bash
php artisan vendor:publish --tag=ichava-config
```

Creates `config/ichava.php`. See [configuration](configuration.md) for the keys.

## 3. Run the migrations

```bash
php artisan migrate
```

Creates the `icons` and `icon_terms` tables (or your configured table prefix).

## 4. Install at least one icon pack

Core ships with no icons. Pick a pack:

```bash
composer require ichava/tabler-icons
# or
composer require ichava/bundled-icons
# or
composer require ichava/metronic-icons
```

Or build your own with `php artisan make:icon-package`. See [creating icon packages](creating-icon-packages.md).

## 5. Seed the icon database

```bash
php artisan ichava:database seed
```

Optional but recommended. The seeder builds the index used by the icon renderer and (if installed) the visual browser. See [database seeding](database-seeding.md).

## 6. Use icons in Blade

```blade
<x-ichava::icon name="ichava/tabler-icons::home" class="w-6 h-6" />
```

Or with the helper:

```blade
{{ ichava('ichava/tabler-icons::home')->color('#4338ca')->class('w-6 h-6') }}
```

## What you get with just core

- `<x-ichava::icon>` Blade component
- `ichava()` global helper
- `ichava:*` Artisan commands
- The icon registry, scaffolder, seeder
- No HTTP routes, no Vue, no Vite

For the visual icon browser at `/ichava/icons` and the REST API, install [`ichava/browser`](../browser/installation.md) on top.

## See also

- [Configuration](configuration.md)
- [Environment variables](environment.md)
- [Database seeding](database-seeding.md)
- [Browser package installation](../browser/installation.md)
- [Troubleshooting](../troubleshooting.md)
