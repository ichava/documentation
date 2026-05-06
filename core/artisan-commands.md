[← Docs](../README.md)

# Artisan Commands Reference

*Reference.*

### Database Commands (`ichava:database`)

```bash
php artisan ichava:database                       # Interactive menu
php artisan ichava:database migrate               # Run migrations
php artisan ichava:database migrate --fresh       # Drop + re-run migrations
php artisan ichava:database seed                  # Seed all packages
php artisan ichava:database seed --package=X      # Seed specific package
php artisan ichava:database seed --sync           # Force synchronous
php artisan ichava:database seed --update         # Force update all (even unchanged)
php artisan ichava:database seed --fresh          # Truncate + seed
php artisan ichava:database seed:icons            # Seed icons only
php artisan ichava:database seed:terms            # Seed terms only
php artisan ichava:database unseed --package=X    # Remove package data
php artisan ichava:database unseed --all          # Remove all data
php artisan ichava:database refresh               # migrate --fresh + seed
php artisan ichava:database truncate              # Truncate tables
php artisan ichava:database stats                 # Show statistics
```

### Cache Commands (`ichava:cache`)

```bash
php artisan ichava:cache clear                   # Clear all caches
php artisan ichava:cache clear --package=X       # Clear package cache
php artisan ichava:cache rebuild                 # Rebuild caches
php artisan ichava:cache refresh                 # Clear + rebuild
php artisan ichava:cache generate                # Generate manifest
php artisan ichava:cache stats                   # Show statistics
```

### Information Commands (`ichava:info`)

```bash
php artisan ichava:info packages                 # List all packages
php artisan ichava:info packages --search=tabler # Search packages
php artisan ichava:info icons                    # List icons
php artisan ichava:info icons --package=X        # Icons in package
php artisan ichava:info icons --search=home      # Search icons
php artisan ichava:info languages                # List FTS languages
php artisan ichava:info discover                 # Discover packages
php artisan ichava:info stats                    # Comprehensive stats
php artisan ichava:info status                   # Lifecycle status
```

### Other Commands

```bash
php artisan ichava:job-status                    # Check seeding-job progress (reads JobProgressTracker)
php artisan ichava:watch                         # Watch icon files for changes (dev)
php artisan make:icon-package                    # Scaffold a new icon package from stubs (interactive)
```

### `make:icon-package`

Generates a complete, production-ready icon package by walking the stub tree at
`stubs/icon-package/` and rendering every file into the destination. All flags
are optional; missing values are prompted for interactively.

```bash
php artisan make:icon-package
php artisan make:icon-package HeroIcons
php artisan make:icon-package HeroIcons --vendor=Acme --email=team@acme.test \
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

### `ichava:cleanup-logs`

Removes Ichava log files older than the configured retention period (`ichava.logging.retention_days`, default 7). The package's scheduler entry runs it daily at the configured `cleanup_time` (default `03:00`); it can also be triggered manually.

```bash
php artisan ichava:cleanup-logs                  # delete logs older than retention_days
php artisan ichava:cleanup-logs --days=14        # override the retention window (one-off)
php artisan ichava:cleanup-logs --dry-run        # report what would be deleted, change nothing
```

### `ichava:inject-npm-scripts`

Adds the Ichava asset-build scripts (`ichava:dev`, `ichava:build`, `ichava:watch`) to the host application's `package.json`. Existing keys are preserved unless `--force` is supplied.

```bash
php artisan ichava:inject-npm-scripts                                 # patches base_path('package.json')
php artisan ichava:inject-npm-scripts --path=/abs/path/to/package.json # custom location
php artisan ichava:inject-npm-scripts --force                          # overwrite if scripts already exist
```

### Programmatic seeding progress

`JobProgressTracker` is a small cache-backed counter readable by the browser UI and `ichava:job-status`. The seeding pipeline writes to it automatically; consumers normally only read.

```php
use Simtabi\Laranail\Ichava\Support\JobProgressTracker;

JobProgressTracker::start('vendor/your-icons', total: 5963);
JobProgressTracker::update('vendor/your-icons', processed: 1500);
JobProgressTracker::complete('vendor/your-icons', meta: ['duration_seconds' => 120]);

$state = JobProgressTracker::status('vendor/your-icons'); // ['total' => …, 'processed' => …, 'state' => …]
```

---

← Previous: [Creating Custom Icon Packages](creating-icon-packages.md) · [Back to README](../README.md) · Next: [Troubleshooting](../troubleshooting.md) →
