# Changelog

All notable changes to this project will be documented in this file.

## [1.0.1] - 2026-05-26

### Docs

- Added migration guide and example configurations to README

### Housekeeping

- Switched publish workflow to npm trusted publishing
- Fixed Node.js version in CI workflows to match engine requirements
- Added funding metadata
- Cleaned up whitespace in `index.js`
- Renamed `readme.md` to `README.md`
- Added `LICENSE` file

## [1.0.0] - 2025-05-26

### Initial Release

Fork of [thncode/homebridge-fakeswitch](https://github.com/thncode/homebridge-fakeswitch) with the following changes:

- Renamed package to `@joshjohanning/homebridge-fakeswitch`
- Updated Node.js engine requirement to `^22.12.0 || ^24.0.0`
- Updated Homebridge engine requirement to `^1.6.0 || ^2.0.0`
- Added CI and publish workflows for automated testing and package publishing
