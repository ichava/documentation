[← Docs](../README.md)

# Artisan Commands Reference

*Reference.*

### Database Commands (`ichava::ichava-core.database`)

```bash
php artisan ichava::ichava-core.database                       # Interactive menu
php artisan ichava::ichava-core.database migrate               # Run migrations
php artisan ichava::ichava-core.database migrate --fresh       # Drop + re-run migrations
php artisan ichava::ichava-core.database seed                  # Seed all packages
php artisan ichava::ichava-core.database seed --package=X      # Seed specific package
php artisan ichava::ichava-core.database seed --sync           # Force synchronous
php artisan ichava::ichava-core.database seed --update         # Force update all (even unchanged)
php artisan ichava::ichava-core.database seed --fresh          # Truncate + seed
php artisan ichava::ichava-core.database seed:icons            # Seed icons only
php artisan ichava::ichava-core.database seed:terms            # Seed terms only
php artisan ichava::ichava-core.database unseed --package=X    # Remove package data
php artisan ichava::ichava-core.database unseed --all          # Remove all data
php artisan ichava::ichava-core.database refresh               # migrate --fresh + seed
php artisan ichava::ichava-core.database truncate              # Truncate tables
php artisan ichava::ichava-core.database stats                 # Show statistics
```

### Cache Commands (`ichava::ichava-core.cache`)

```bash
php artisan ichava::ichava-core.cache clear                   # Clear all caches
php artisan ichava::ichava-core.cache clear --package=X       # Clear package cache
php artisan ichava::ichava-core.cache rebuild                 # Rebuild caches
php artisan ichava::ichava-core.cache refresh                 # Clear + rebuild
php artisan ichava::ichava-core.cache generate                # Generate manifest
php artisan ichava::ichava-core.cache stats                   # Show statistics
```

### Information Commands (`ichava::ichava-core.info`)

```bash
php artisan ichava::ichava-core.info packages                 # List all packages
php artisan ichava::ichava-core.info packages --search=tabler # Search packages
php artisan ichava::ichava-core.info icons                    # List icons
php artisan ichava::ichava-core.info icons --package=X        # Icons in package
php artisan ichava::ichava-core.info icons --search=home      # Search icons
php artisan ichava::ichava-core.info languages                # List FTS languages
php artisan ichava::ichava-core.info discover                 # Discover packages
php artisan ichava::ichava-core.info stats                    # Full stats
php artisan ichava::ichava-core.info status                   # Lifecycle status
```

### Other Commands

```bash
php artisan ichava::ichava-core.job-status                    # Check seeding-job progress (reads JobProgressTracker)
php artisan ichava::ichava-core.watch                         # Watch icon files for changes (dev)
php artisan ichava::ichava-core.make:icon-package                    # Scaffold a new icon package from stubs (interactive)
```

### `ichava::ichava-core.make:icon-package`

Generates a complete, production-ready icon package by walking the stub tree at
`stubs/icon-package/` and rendering every file into the destination. All flags
are optional; missing values are prompted for interactively.

```bash
php artisan ichava::ichava-core.make:icon-package
php artisan ichava::ichava-core.make:icon-package HeroIcons
php artisan ichava::ichava-core.make:icon-package HeroIcons --vendor=Acme --email=team@acme.test \
    --prefix=hi --type=multi --variants=outline,solid \
    --path=ichava-hero-icons --force
```

| Flag | Effect |
|---|---|
| `name` (positional) | StudlyCase package short-name (e.g. `Hero`, `Tabler`). The literal `Icons` suffix is appended automatically by the stubs, pass `Hero`, *not* `HeroIcons`. |
| `--vendor=` | Vendor for namespace + composer name. Auto-normalised: `your company` → namespace `YourCompany`, composer `your-company`. |
| `--email=` | Author email for `composer.json` and `config.json`. |
| `--path=` | Destination directory (absolute, or relative to `base_path()`). Parent will be created if missing. |
| `--prefix=` | Blade-component prefix; defaults to the kebab form of `name`. |
| `--type=` | `single` (default), flat `files/` directory; or `multi`, one sub-directory per variant. |
| `--variants=` | Comma-separated list of variant slugs when `--type=multi` (e.g. `outline,solid,filled`). |
| `--force` | Overwrite an existing destination without confirmation. |

The full stub system, placeholder reference, customising / adding stubs, is
documented in [Creating Custom Icon Packages](creating-icon-packages.md).

### `ichava::ichava-core.cleanup-logs`

Removes Ichava log files older than the configured retention period (`ichava.logging.retention_days`, default 7). The package's scheduler entry runs it daily at the configured `cleanup_time` (default `03:00`); it can also be triggered manually.

```bash
php artisan ichava::ichava-core.cleanup-logs                  # delete logs older than retention_days
php artisan ichava::ichava-core.cleanup-logs --days=14        # override the retention window (one-off)
php artisan ichava::ichava-core.cleanup-logs --dry-run        # report what would be deleted, change nothing
```

### `ichava::ichava-core.icons:check-updates`

Reports whether any registered icon pack is behind its upstream source. Reads each pack's `upstream` block from its `config.json`, hits the declared `version_check_url` (npm registry, GitHub releases / tags, Packagist, or a custom URL), and prints a status table. Dispatches `IconPackUpdateAvailable` events for stale packs so host apps can wire Slack / email / dashboard notifications.

```bash
php artisan ichava::ichava-core.icons:check-updates                              # table for every pack
php artisan ichava::ichava-core.icons:check-updates --package=ichava/emoji-sets  # restrict to one pack
php artisan ichava::ichava-core.icons:check-updates --format=json                # machine-readable
php artisan ichava::ichava-core.icons:check-updates --fail-on-stale              # exit 1 if any pack is behind
```

| Arg / Flag | Effect |
|---|---|
| `--package=` | Restrict to one `vendor/name` pack (else: every pack in `IconRegistry`). |
| `--format=table\|json` | Output shape. `json` is what CI scripts consume. |
| `--fail-on-stale` | Exit non-zero when any pack is behind or unreachable. |

Refreshing the actual SVG assets is **not** an end-user step -- `vendor/` is regenerated on every `composer install`. The maintainer-side refresh runs in CI via [`ichava/maintainer-toolkit`](https://github.com/ichava/maintainer-toolkit); see [`../icon-pack-maintainer-sync.md`](../icon-pack-maintainer-sync.md).

### `ichava:inject-npm-scripts`

Adds the Ichava asset-build scripts (`ichava:dev`, `ichava:build`, `ichava::ichava-core.watch`) to the host application's `package.json`. Existing keys are preserved unless `--force` is supplied.

```bash
php artisan ichava:inject-npm-scripts                                 # patches base_path('package.json')
php artisan ichava:inject-npm-scripts --path=/abs/path/to/package.json # custom location
php artisan ichava:inject-npm-scripts --force                          # overwrite if scripts already exist
```

### Programmatic seeding progress

`JobProgressTracker` is a small cache-backed counter readable by the browser UI and `ichava::ichava-core.job-status`. The seeding pipeline writes to it automatically; consumers normally only read.

```php
use Simtabi\Laranail\Ichava\Support\JobProgressTracker;

JobProgressTracker::start('vendor/your-icons', total: 5963);
JobProgressTracker::update('vendor/your-icons', processed: 1500);
JobProgressTracker::complete('vendor/your-icons', meta: ['duration_seconds' => 120]);

$state = JobProgressTracker::status('vendor/your-icons'); // ['total' => …, 'processed' => …, 'state' => …]
```

---

← Previous: [Creating Custom Icon Packages](creating-icon-packages.md) · [Back to README](../README.md) · Next: [Troubleshooting](../troubleshooting.md) →
