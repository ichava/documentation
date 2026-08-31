[← Docs](../README.md)

# Building your own icon pack

*Tutorial.*

You can ship your own icon pack as a Composer package and have it work alongside `ichava/tabler-icons` and the others. The fastest path is the `make:icon-package` scaffolder shipped with `ichava/core`.

## 1. Run the scaffolder

In a host Laravel app that has `ichava/core` installed:

```bash
php artisan make:icon-package
```

Or non-interactively:

```bash
php artisan make:icon-package Hero \
    --vendor=Acme \
    --email=team@acme.test \
    --prefix=hi \
    --type=multi \
    --variants=outline,solid \
    --path=ichava-hero-icons
```

You get a complete package: `composer.json`, service provider, constants class, variant enum, Blade component, update command, `config.json`, README, CHANGELOG, LICENSE, `phpunit.xml.dist`, and a `docs/` directory pre-populated with vendor-specific stubs.

See [`make:icon-package` reference](../core/creating-icon-packages.md) for every flag and token.

## 2. Drop in your SVGs

Single-style packs:

```
resources/assets/svg/files/
├── home.svg
├── user.svg
└── settings.svg
```

Multi-variant packs:

```
resources/assets/svg/files/
├── outline/
│   └── home.svg
└── solid/
    └── home.svg
```

## 3. Edit `config.json`

`resources/assets/svg/config.json` declares your pack's metadata: name, description, variants, default class, prefix. The `IconsConstants` class reads this at runtime.

## 4. Write your pack-specific docs

The scaffolder seeded `docs/` for you. Fill in:

- `docs/variants.md`, what your variants are and when to use each
- `docs/customization.md`, knobs unique to your pack (stroke width, currentColor, sizing)
- `docs/attribution.md`, upstream credits + licence

Cross-link to the main documentation for shared concerns:

```markdown
For the icon path grammar, see
https://github.com/ichava/documentation/blob/main/core/icon-path-format.md
```

## 5. Tag and publish

```bash
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main v1.0.0
```

Submit to [Packagist](https://packagist.org) so users can `composer require <vendor>/<pkg>`.

## Conventions you inherit

Every Ichava pack follows the same shape:

- Class short names are constants (`IconsServiceProvider`, `IconsConstants`, `Variant` or `Category`, `IconComponent`). Disambiguation is by namespace.
- Composer name is `<vendor>/<short>-icons`. GitHub repo is `<vendor>/<short>-icons` (no extra prefix).
- Pack-specific docs live in `docs/`. Shared concerns link back to `ichava/documentation`.
- Tag releases as `v<x.y.z>`.

## See also

- [`make:icon-package` flag reference](../core/creating-icon-packages.md)
- [Icon path format](../core/icon-path-format.md)
- [Database seeding](../core/database-seeding.md)
- [Custom icon sets (in-app, no package)](../core/custom-icon-sets.md)
