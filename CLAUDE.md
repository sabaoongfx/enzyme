# Enzyme Modern

Modernized fork of [enzyme](https://github.com/enzymejs/enzyme) — React testing utilities.

## npm

- **Org**: sabaoongfx (https://www.npmjs.com/settings/sabaoongfx/profile)
- **Team**: Developers (default, read/write access to all org packages)
- **Registry**: https://registry.npmjs.org/

## Packages

| Package | Version | npm Name |
|---------|---------|----------|
| Core | 4.0.1 | `enzyme-modern` |
| Shallow Equal | 1.0.7 | `enzyme-modern-shallow-equal` |
| Adapter Utils | 1.14.2 | `enzyme-modern-adapter-utils` |
| Adapter React 16 | 1.15.8 | `enzyme-modern-adapter-react-16` |

## Publish Order

Dependencies must be published in this order:

1. `enzyme-modern-shallow-equal` (no internal deps)
2. `enzyme-modern` (depends on shallow-equal)
3. `enzyme-modern-adapter-utils` (utility package)
4. `enzyme-modern-adapter-react-16` (depends on all above)

## Publish Command

```bash
cd packages/<package> && npm run build && npm publish --ignore-scripts
```

## Git

- **Repo**: https://github.com/sabaoongfx/enzyme
- **Branch**: master
- **Author**: sabaoongfx <sabaoongfx@gmail.com>

## Tech Stack

- Lerna 2.11.0 monorepo (independent versioning)
- Babel 7 with airbnb preset
- Mocha + Chai + Sinon for tests
- ESLint 8 with airbnb config

## Current State

- React 16 support only (adapters for 0.13 through 16.x)
- No React 17/18/19 adapters yet — this is the main goal of the fork
