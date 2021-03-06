# recommended-bump [![npm version][npmv-img]][npmv-url] [![github release][ghrelease-img]][ghrelease-url] [![License][license-img]][license-url]
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FtunnckoCoreLabs%2Frecommended-bump.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FtunnckoCoreLabs%2Frecommended-bump?ref=badge_shield)

> Calculates recommended bump (next semver version) based on given array of commit messages following Conventional Commits specification

Please consider following this project's author, [Charlike Mike Reagent](https://github.com/tunnckoCore), and :star: the project to show your :heart: and support.

<div id="thetop"></div>

[![Code style][codestyle-img]][codestyle-url]
[![CircleCI linux build][linuxbuild-img]][linuxbuild-url]
[![CodeCov coverage status][codecoverage-img]][codecoverage-url]
[![DavidDM dependency status][dependencies-img]][dependencies-url]
[![Renovate App Status][renovateapp-img]][renovateapp-url]
[![Make A Pull Request][prs-welcome-img]][prs-welcome-url]
[![Semantically Released][new-release-img]][new-release-url]

If you have any _how-to_ kind of questions, please read the [Contributing Guide](./CONTRIBUTING.md) and [Code of Conduct](./CODE_OF_CONDUCT.md) documents.  
For bugs reports and feature requests, [please create an issue][open-issue-url] or ping
[@tunnckoCore](https://twitter.com/tunnckoCore) at Twitter.

[![Become a Patron][patreon-img]][patreon-url]
[![Conventional Commits][ccommits-img]][ccommits-url]
[![NPM Downloads Weekly][downloads-weekly-img]][npmv-url]
[![NPM Downloads Monthly][downloads-monthly-img]][npmv-url]
[![NPM Downloads Total][downloads-total-img]][npmv-url]
[![Share Love Tweet][shareb]][shareu]

Project is [semantically](https://semver.org) & automatically released on [CircleCI](https://circleci.com) with [new-release][] and its [New Release](https://github.com/apps/new-release) GitHub App.

<!-- Logo when needed:

<p align="center">
  <a href="https://github.com/tunnckoCoreLabs/recommended-bump">
    <img src="./media/logo.png" width="85%">
  </a>
</p>

-->

## Table of Contents

- [Install](#install)
- [API](#api)
  * [src/index.js](#srcindexjs)
    + [recommendedBump](#recommendedbump)
- [See Also](#see-also)
- [Contributing](#contributing)
  * [Follow the Guidelines](#follow-the-guidelines)
  * [Support the project](#support-the-project)
  * [OPEN Open Source](#open-open-source)
  * [Wonderful Contributors](#wonderful-contributors)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install

This project requires [**Node.js**](https://nodejs.org) **^8.10.0 || >=10.13.0**. Install it using
[**yarn**](https://yarnpkg.com) or [**npm**](https://npmjs.com).  
_We highly recommend to use Yarn when you think to contribute to this project._

```bash
$ yarn add recommended-bump
```

## API

<!-- docks-start -->
_Generated using [docks](http://npm.im/docks)._

### [src/index.js](/src/index.js)

#### [recommendedBump](/src/index.js#L62)
Calculates recommended bump (next version), based on given `commits`.
It always returns an object. If no commits are given it is `{ increment: false }`.
Otherwise it may contain `patch`, `minor`, or `major` properties which are
of `Array<Commit>` type, based on [parse-commit-message][].

ProTip: Use `result[result.increment]` to get most meanigful result.

Each item passed as `commits` is validated against the Convetional Comits Specification
and using [parse-commit-message][]. Commits can be string, array of commit message strings,
array of objects (of [type Commit as defined](https://github.com/tunnckoCoreLabs/parse-commit-message#type-definitions)) or mix of previous
posibilities.

See the tests and examples for more clarity.

**Params**
- `commits` **{string||}** commit messages one of `string`, `Array<string>` or `Array<Commit>`
- `[options]` **{object}** pass additional `options.plugins` to be passed to [parse-commit-message][]

**Returns**
- `object` result like `{ increment: boolean | string, patch?, minor?, major? }`

**Examples**
```javascript
import recommendedBump from 'recommended-bump';

const commits = [
  'chore: foo bar baz',
  `fix(cli): some bugfix msg here

Some awesome body.

Great footer and GPG sign off, yeah!
Signed-off-by: Awesome footer <foobar@gmail.com>`
  ];

const { increment, isBreaking, patch } = recommendedBump(commits);

console.log(isBreaking); // => false
console.log(increment); // => 'patch'
console.log(patch);
// => [{ header: { type, scope, subject }, body, footer }, { ... }]
console.log(patch[0].header.type); // => 'fix'
console.log(patch[0].header.scope); // => 'cli'
console.log(patch[0].header.subject); // => 'some bugfix msg here'
console.log(patch[0].body); // => 'Some awesome body.'
console.log(patch[0].footer);
// => 'Great footer and GPG sign off, yeah!\nSigned-off-by: Awesome footer <foobar@gmail.com>'
```
```javascript
import { parse } from 'parse-commit-message';
import recommendedBump from 'recommended-bump';

const commitOne = parse('fix: foo bar');
const commitTwo = parse('feat: some feature subject');

const result = recommendedBump([commitOne, commitTwo]);
console.log(result.increment); // => 'minor'
console.log(result.isBreaking); // => false
console.log(result.minor); // => [{ ... }]
```

<!-- docks-end -->

**[back to top](#thetop)**

## See Also

Some of these projects are used here or were inspiration for this one, others are just related. So, thanks for your existance!

- [@tunnckocore/config](https://www.npmjs.com/package/@tunnckocore/config): All the configs for all the tools, in one place | [homepage](https://github.com/tunnckoCoreLabs/config "All the configs for all the tools, in one place")
- [@tunnckocore/create-project](https://www.npmjs.com/package/@tunnckocore/create-project): Create and scaffold a new project, its GitHub repository and contents | [homepage](https://github.com/tunnckoCoreLabs/create-project "Create and scaffold a new project, its GitHub repository and contents")
- [@tunnckocore/execa](https://www.npmjs.com/package/@tunnckocore/execa): Thin layer on top of [execa][] that allows executing multiple commands… [more](https://github.com/tunnckoCoreLabs/execa) | [homepage](https://github.com/tunnckoCoreLabs/execa "Thin layer on top of [execa][] that allows executing multiple commands in parallel or in sequence")
- [@tunnckocore/package-json](https://www.npmjs.com/package/@tunnckocore/package-json): Simple and fast getting of latest package.json metadata for a npm… [more](https://github.com/tunnckoCoreLabs/package-json) | [homepage](https://github.com/tunnckoCoreLabs/package-json "Simple and fast getting of latest package.json metadata for a npm module, using axios and unpkg as a source, because npm registry is basically slow")
- [@tunnckocore/scripts](https://www.npmjs.com/package/@tunnckocore/scripts): Universal and minimalist scripts & tasks runner. | [homepage](https://github.com/tunnckoCoreLabs/scripts "Universal and minimalist scripts & tasks runner.")
- [@tunnckocore/update](https://www.npmjs.com/package/@tunnckocore/update): Update to latest project files and templates, based on `charlike` scaffolder | [homepage](https://github.com/tunnckoCoreLabs/update "Update to latest project files and templates, based on `charlike` scaffolder")
- [asia](https://www.npmjs.com/package/asia): Blazingly fast, magical and minimalist testing framework, for Today and Tomorrow | [homepage](https://github.com/olstenlarck/asia#readme "Blazingly fast, magical and minimalist testing framework, for Today and Tomorrow")
- [charlike](https://www.npmjs.com/package/charlike): Small, fast and streaming project scaffolder with support for hundreds of… [more](https://github.com/tunnckoCoreLabs/charlike) | [homepage](https://github.com/tunnckoCoreLabs/charlike "Small, fast and streaming project scaffolder with support for hundreds of template engines and sane defaults")
- [docks](https://www.npmjs.com/package/docks): Extensible system for parsing and generating documentation. It just freaking works! | [homepage](https://github.com/tunnckoCore/docks "Extensible system for parsing and generating documentation. It just freaking works!")
- [gitcommit](https://www.npmjs.com/package/gitcommit): Lightweight and joyful `git commit` replacement. Conventional Commits compliant. | [homepage](https://github.com/tunnckoCore/gitcommit "Lightweight and joyful `git commit` replacement. Conventional Commits compliant.")

**[back to top](#thetop)**

## Contributing

### Follow the Guidelines

Please read the [Contributing Guide](./CONTRIBUTING.md) and [Code of Conduct](./CODE_OF_CONDUCT.md) documents for advices.  
For bugs reports and feature requests, [please create an issue][open-issue-url] or ping
[@tunnckoCore](https://twitter.com/tunnckoCore) at Twitter.

### Support the project

[Become a Partner or Sponsor?][patreon-url] :dollar: Check the **Partner**, **Sponsor** or **Omega-level** tiers! :tada: You can get your company logo, link & name on this file. It's also rendered on package page in [npmjs.com][npmv-url] and [yarnpkg.com](https://yarnpkg.com/en/package/recommended-bump) sites too! :rocket:

Not financial support? Okey! [Pull requests](https://github.com/tunnckoCoreLabs/contributing#opening-a-pull-request), stars and all kind of [contributions](https://opensource.guide/how-to-contribute/#what-it-means-to-contribute) are always
welcome. :sparkles:

### OPEN Open Source

This project is following [OPEN Open Source](http://openopensource.org) model

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is built on collective efforts and it's not strongly guarded by its founders.

There are a few basic ground-rules for its contributors

1. Any **significant modifications** must be subject to a pull request to get feedback from other contributors.
2. [Pull requests](https://github.com/tunnckoCoreLabs/contributing#opening-a-pull-request) to get feedback are _encouraged_ for any other trivial contributions, but are not required.
3. Contributors should attempt to adhere to the prevailing code-style and development workflow.

### Wonderful Contributors

Thanks to the hard work of these wonderful people this project is alive! It follows the
[all-contributors](https://github.com/kentcdodds/all-contributors) specification.  
Don't hesitate to add yourself to that list if you have made any contribution! ;) [See how,
here](https://github.com/jfmengels/all-contributors-cli#usage).

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
| [<img src="https://avatars3.githubusercontent.com/u/5038030?v=4" width="120px;"/><br /><sub><b>Charlike Mike Reagent</b></sub>](https://tunnckocore.com)<br />[💻](https://github.com/tunnckoCoreLabs/recommended-bump/commits?author=tunnckoCore "Code") [📖](https://github.com/tunnckoCoreLabs/recommended-bump/commits?author=tunnckoCore "Documentation") [💬](#question-tunnckoCore "Answering Questions") [👀](#review-tunnckoCore "Reviewed Pull Requests") [🔍](#fundingFinding-tunnckoCore "Funding Finding") |
| :---: |

<!-- ALL-CONTRIBUTORS-LIST:END -->

Consider showing your [support](#support-the-project) to them. :sparkling_heart:

## License

Copyright (c) 2018-present, [Charlike Mike Reagent](https://tunnckocore.com) `<mameto2011@gmail.com>` & [contributors](#wonderful-contributors).  
Released under the [Apache-2.0 License][license-url].

<!-- Heading badges -->

[npmv-url]: https://www.npmjs.com/package/recommended-bump
[npmv-img]: https://badgen.net/npm/v/recommended-bump?icon=npm

[ghrelease-url]: https://github.com/tunnckoCoreLabs/recommended-bump/releases/latest
[ghrelease-img]: https://badgen.net/github/release/tunnckoCoreLabs/recommended-bump?icon=github

[license-url]: https://github.com/tunnckoCoreLabs/recommended-bump/blob/master/LICENSE
[license-img]: https://badgen.net/npm/license/recommended-bump

<!-- Front line badges -->

[codestyle-url]: https://github.com/airbnb/javascript
[codestyle-img]: https://badgen.net/badge/code%20style/airbnb/ff5a5f?icon=airbnb

[linuxbuild-url]: https://circleci.com/gh/tunnckoCoreLabs/recommended-bump/tree/master
[linuxbuild-img]: https://badgen.net/circleci/github/tunnckoCoreLabs/recommended-bump/master?label=build&icon=circleci

[codecoverage-url]: https://codecov.io/gh/tunnckoCoreLabs/recommended-bump
[codecoverage-img]: https://badgen.net/codecov/c/github/tunnckoCoreLabs/recommended-bump?icon=codecov

[dependencies-url]: https://david-dm.org/tunnckoCoreLabs/recommended-bump
[dependencies-img]: https://badgen.net/david/dep/tunnckoCoreLabs/recommended-bump?label=deps

[ccommits-url]: https://conventionalcommits.org/
[ccommits-img]: https://badgen.net/badge/conventional%20commits/v1.0.0/dfb317
[new-release-url]: https://ghub.io/new-release
[new-release-img]: https://badgen.net/badge/semantically/released/05c5ff

[downloads-weekly-img]: https://badgen.net/npm/dw/recommended-bump
[downloads-monthly-img]: https://badgen.net/npm/dm/recommended-bump
[downloads-total-img]: https://badgen.net/npm/dt/recommended-bump

[renovateapp-url]: https://renovatebot.com
[renovateapp-img]: https://badgen.net/badge/renovate/enabled/green
[prs-welcome-img]: https://badgen.net/badge/PRs/welcome/green
[prs-welcome-url]: http://makeapullrequest.com
[paypal-donate-url]: https://paypal.me/tunnckoCore/10
[paypal-donate-img]: https://badgen.net/badge/$/support/purple
[patreon-url]: https://www.patreon.com/bePatron?u=5579781
[patreon-img]: https://badgen.net/badge/patreon/tunnckoCore/F96854?icon=patreon
[patreon-sponsor-img]: https://badgen.net/badge/become/a%20sponsor/F96854?icon=patreon

[shareu]: https://twitter.com/intent/tweet?text=https://github.com/tunnckoCoreLabs/recommended-bump&via=tunnckoCore
[shareb]: https://badgen.net/badge/twitter/share/1da1f2?icon=twitter
[open-issue-url]: https://github.com/tunnckoCoreLabs/recommended-bump/issues/new

[execa]: https://github.com/sindresorhus/execa
[new-release]: https://github.com/tunnckoCore/new-release
[parse-commit-message]: https://github.com/tunnckoCoreLabs/parse-commit-message

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FtunnckoCoreLabs%2Frecommended-bump.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FtunnckoCoreLabs%2Frecommended-bump?ref=badge_large)