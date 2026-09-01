# Changelog

All notable changes to the Ichava documentation follow [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

This repository ships prose rather than code, so a version here marks a state of the documentation
rather than a release anyone installs.

## [0.1.0] - 2026-08-31

First open-source release, alongside every other package in the ecosystem.

### Added

- Cross-cutting pages: architecture, security model, STRIDE threat model, troubleshooting,
  upstream tracking and maintainer sync.
- Per-package guides for `ichava/core` and `ichava/browser`, and shared guides for icon packs.
- The package table, topology diagram and docs map now cover all eleven repositories.

### Fixed

- **Every install command worked only in theory.** Nothing in the ecosystem is on Packagist, so
  `composer require ichava/core` fails. The installation pages and the hub now open with the VCS
  repositories a host has to declare, the three unpublished `laranail/*` packages included.
- Config surface brought in line with what ships: `config('ichava.core.*')`,
  `--tag=ichava::core-config`, and the nested published path `config/ichava/core.php`.
- The security model described a policy the ecosystem replaced, an unconditional block on `href`
  and `xlink:href`. It now documents blocking by value, the two passes that run before
  sanitisation, and the recovery pass for malformed author input.
- The provider class diagram showed `TablerIconsServiceProvider` and friends. Every pack's provider
  is `IconsServiceProvider`, disambiguated by namespace, which is the convention the diagram exists
  to illustrate.
- Icon counts replaced with measured ones: 6,184 tabler, 121,314 bundled across 72 sets, 501
  metronic, 542 flag.
