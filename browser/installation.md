[← Docs](../README.md)

# Installation

*How-to guide.*

`ichava/browser` is the optional HTTP layer for Ichava: visual icon browser SPA + REST API + middleware. Install it on top of [`ichava/core`](../core/installation.md).

## 1. Require the package

```bash
composer require ichava/browser
```

The `IchavaBrowserServiceProvider` registers automatically. The browser depends on `ichava/core`, so Composer pulls it transitively if you don't already have it.

## 2. Publish the browser config

```bash
php artisan vendor:publish --tag=ichava-browser-config
```

Creates `config/ichava-browser.php`. See [configuration](configuration.md) for the keys.

## 3. Publish the SPA assets

```bash
php artisan vendor:publish --tag=ichava-assets
```

Copies the pre-built Vite output (`ichava.js`, `ichava.css`, source maps) into `public/vendor/ichava/`. Do this after every `composer update` of the package.

## 4. Visit the browser

```
http://example.com/ichava/icons
```

The prefix (`ichava` by default) is set by `ICHAVA_BROWSER_PREFIX`. The same prefix is shared with core's REST API at `/ichava/api/...`.

## 5. (Optional) Inject npm scripts for development

If you want to rebuild the SPA yourself:

```bash
php artisan ichava:inject-npm-scripts
```

Adds `ichava:dev`, `ichava:build`, and `ichava:watch` to your host app's `package.json`. Run `npm run ichava:dev` for the Vite dev server with HMR, or `npm run ichava:build` for a production bundle.

You only need this if you customise the SPA. End users running pre-built assets do not.

## What you get on top of core

- The Vue + Vite icon-browser SPA at `/{prefix}/icons`
- The REST API at `/{prefix}/api/...` (icons, packages, terms, preferences, cache)
- All Ichava middleware (`ichava.api`, `ichava.web`, hybrid Sanctum/session detection)
- The `<x-ichava::ichava-test-icons>` and `<x-ichava::ichava-ui-icons>` demo Blade components
- The `ui-icons` icon set used by the SPA
- The `ichava:inject-npm-scripts` Artisan command

## See also

- [Configuration](configuration.md)
- [Environment variables](environment.md)
- [API endpoints](api-endpoints.md)
- [shadcn-vue installer](shadcn-installer.md)
- [Core installation](../core/installation.md)
- [Troubleshooting](../troubleshooting.md)
