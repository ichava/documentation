[← Docs](../README.md)

# Installation

*How-to guide.*

## 1. Point Composer at the repositories

**Nothing in the Ichava ecosystem is published on Packagist yet.** `composer require ichava/core`
on its own fails with "could not be found". Add the VCS repositories to your application's
`composer.json` first, including the three `laranail/*` packages core depends on, which are also
unpublished:

```json
{
    "repositories": [
        { "type": "vcs", "url": "https://github.com/ichava/core" },
        { "type": "vcs", "url": "https://github.com/laranail/package-tools.git" },
        { "type": "vcs", "url": "https://github.com/laranail/console.git" },
        { "type": "vcs", "url": "https://github.com/laranail/enumerator.git" }
    ]
}
```

Composer reads `repositories` only from the root package, so a package's own entries do not carry
across to yours: every unpublished package in the tree has to be named here, core's dependencies
included.

## 2. Require the package

```bash
composer require ichava/core:^0.1
```

The `IchavaServiceProvider` registers automatically via Laravel package discovery.

## 3. Publish the config

```bash
php artisan vendor:publish --tag=ichava::core-config
```

Creates `config/ichava/core.php`. See [configuration](configuration.md) for the keys.

## 4. Run the migrations

```bash
php artisan migrate
```

Creates the `icons` and `icon_terms` tables (or your configured table prefix).

## 5. Install at least one icon pack

Core ships with no icons. The publicly available packs are:

| Pack | Icons | Add this repository |
|---|---|---|
| `ichava/tabler-icons` | 6,184 | `https://github.com/ichava/tabler-icons` |
| `ichava/flag-icons` | 542 | `https://github.com/ichava/flag-icons` |
| `ichava/emoji-sets` | engine wiring only, assets pending | `https://github.com/ichava/emoji-sets` |

```bash
composer require ichava/tabler-icons:^0.1
```

`ichava/bundled-icons` (121,314 icons) and `ichava/metronic-icons` (501) are **private**: they are
part of the ecosystem but not distributable, so they are available only to accounts with access.

Or build your own with `php artisan ichava::ichava-core.make:icon-package`. See [creating icon packages](creating-icon-packages.md).

## 6. Seed the icon database

```bash
php artisan ichava::ichava-core.database seed
```

Optional but recommended. The seeder builds the index used by the icon renderer and (if installed) the visual browser. See [database seeding](database-seeding.md).

## 7. Use icons in Blade

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
