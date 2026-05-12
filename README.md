# Ichava documentation

Long-form documentation for the Ichava Laravel icon ecosystem. Plain markdown, browseable directly on GitHub.

## Packages

| Repo | Role |
|---|---|
| [`ichava/core`](https://github.com/ichava/core) | Engine. Services, registry, seeder, Blade base component, scaffolder, migrations. No HTTP surface, no JS toolchain. |
| [`ichava/browser`](https://github.com/ichava/browser) | HTTP layer. REST API, Vue/Vite SPA, Blade browser views, middleware. Optional. |
| [`ichava/tabler-icons`](https://github.com/ichava/tabler-icons) | 5,900+ Tabler icons (outline + filled). |
| [`ichava/bundled-icons`](https://github.com/ichava/bundled-icons) | 121,000+ icons across 70+ open-source sets. |
| [`ichava/metronic-icons`](https://github.com/ichava/metronic-icons) | 500+ Metronic icons (brand logos, flags, file types, illustrations). |
| `ichava/ichava` *(planned)* | Marketing landing + Composer metapackage. |

## Install

```bash
# Engine + visual UI + an icon pack
composer require ichava/core ichava/browser ichava/tabler-icons

# Headless engine only (no UI, no API)
composer require ichava/core ichava/tabler-icons
```

See [`core/installation.md`](core/installation.md) and [`browser/installation.md`](browser/installation.md) for the full setup.

## Documentation map

Documentation is grouped by repo. Cross-cutting topics (architecture, security, troubleshooting) live at the top level.

### Cross-cutting

- [Architecture](architecture.md), how the packages relate
- [Security model](security-model.md), threat model and mitigations
- [Security threat model](security-threat-model.md), STRIDE walkthrough and disclosure SLAs
- [Troubleshooting](troubleshooting.md), common issues
- [Icon-pack upstream tracking](icon-pack-upstream-tracking.md), host-app side -- how to subscribe to update events
- [Icon-pack maintainer sync](icon-pack-maintainer-sync.md), maintainer side -- how we refresh vendored assets and ship a new release
- [Contributing](CONTRIBUTING.md), style guide and PR conventions
- [Security policy](SECURITY.md), how to report a vulnerability

### `ichava/core` (engine)

- [Installation](core/installation.md)
- [Configuration](core/configuration.md), `config/ichava.php` keys
- [Environment variables](core/environment.md), every `ICHAVA_*` engine env var
- [Icon path format](core/icon-path-format.md), the `vendor/pkg::category/icon` grammar
- [Blade components](core/blade-components.md), the base `<x-ichava::icon>`
- [Global helper](core/global-helper.md), the `ichava()` fluent function
- [Artisan commands](core/artisan-commands.md), every `ichava:*` command
- [Database seeding](core/database-seeding.md), queue-backed seeder + dedup
- [Custom icon sets](core/custom-icon-sets.md), in-app sets without a package
- [Creating icon packages](core/creating-icon-packages.md), the `make:icon-package` scaffolder

### `ichava/browser` (HTTP layer)

- [Installation](browser/installation.md)
- [Configuration](browser/configuration.md), `config/ichava-browser.php` keys
- [Environment variables](browser/environment.md), browser-specific env vars
- [API endpoints](browser/api-endpoints.md), REST endpoint reference
- [shadcn-vue installer](browser/shadcn-installer.md), `.dev/shadcn_vue_installer.sh`

### Icon packs

- [Using an icon pack](icon-packs/using-an-icon-pack.md), install and render any pack
- [Seeding pack icons](icon-packs/seeding-pack-icons.md), when and how to seed
- [Building your own pack](icon-packs/building-your-own.md), the scaffolder walkthrough

Pack-specific content (variants, attribution, customisation) lives inside each pack's repo at `docs/`. Every pack follows the same shape:

```
<pack-repo>/
├── README.md          install + quick example + link here
└── docs/
    ├── README.md      pack-specific TOC
    ├── variants.md    or categories.md
    ├── customization.md
    └── attribution.md upstream license + credits
```

Pack docs link back to this directory for shared concerns. When you build your own pack with `make:icon-package`, the scaffolder generates `docs/` for you.

Examples:

- [`ichava/tabler-icons/docs/`](https://github.com/ichava/tabler-icons/tree/main/docs)
- [`ichava/bundled-icons/docs/`](https://github.com/ichava/bundled-icons/tree/main/docs)
- [`ichava/metronic-icons/docs/`](https://github.com/ichava/metronic-icons/tree/main/docs)

## Contributing

Pull requests welcome. Plain CommonMark, no static-site builder yet. See [CONTRIBUTING.md](CONTRIBUTING.md) for the style guide.

## License

This project is licensed under the MIT License.  

© Simtabi LLC
