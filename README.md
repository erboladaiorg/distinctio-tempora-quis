# option

[![deno land](http://img.shields.io/badge/available%20on-deno.land/x-lightgrey.svg?logo=deno)](https://deno.land/x/optio)
[![deno doc](https://doc.deno.land/badge.svg)](https://deno.land/x/optio?doc)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/erboladaiorg/distinctio-tempora-quis)](https://github.com/erboladaiorg/distinctio-tempora-quis/releases)
[![codecov](https://codecov.io/github/erboladaiorg/distinctio-tempora-quis/branch/main/graph/badge.svg)](https://codecov.io/gh/erboladaiorg/distinctio-tempora-quis)
[![License](https://img.shields.io/github/license/erboladaiorg/distinctio-tempora-quis)](LICENSE)

[![test](https://github.com/erboladaiorg/distinctio-tempora-quis/actions/workflows/test.yaml/badge.svg)](https://github.com/erboladaiorg/distinctio-tempora-quis/actions/workflows/test.yaml)
[![NPM](https://nodei.co/npm/@erboladaiorg/distinctio-tempora-quis.png?mini=true)](https://nodei.co/npm/@erboladaiorg/distinctio-tempora-quis/)
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg)](https://github.com/RichardLitt/standard-readme)
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

Minimum option type port of Rust.

## Table of Contents <!-- omit in toc -->

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [Feature](#feature)
- [API](#api)
- [Acknowledgements](#acknowledgements)
- [Contributing](#contributing)
- [License](#license)

## Background

This project provides minimum option features. They are designed to be optimized
in tree-shaking.

One of the existing challenges in the JavaScript/TypeScript community is
tree-shaking. Due to the dynamic nature of the language, tree-shaking can only
be used in limited situations. That is, tree-shaking cannot do anything about
unused class methods or properties.

The only solution to this is separation into top-level functions. It is very
unfortunate but true that no other method exists.

Having said that, a [future proposal](#feature) could solve this.

## Install

deno.land:

```ts
import * as mod from "https://deno.land/x/optio/mod.ts";
```

npm:

```bash
npm i @erboladaiorg/distinctio-tempora-quis
```

## Usage

Type [Option](https://deno.land/x/optio/mod.ts?s=Option) represents an optional
value.

Every [Option](https://deno.land/x/optio/mod.ts?s=Option) is either
[Some](https://deno.land/x/optio/mod.ts?s=Some) and contains a value, or
[None](https://deno.land/x/optio/mod.ts?s=None), and does not.

```ts
import {
  expect,
  None,
  type Option,
  Some,
} from "https://deno.land/x/optio/mod.ts";

function divide(numerator: number, denominator: number): Option<number> {
  if (!denominator) return None;

  return Some(numerator / denominator);
}

const opt = divide(100, 0);
expect(opt, "divide by 0");
```

All [operators](https://deno.land/x/optio/mod.ts#Functions) for
[Option](https://deno.land/x/optio/mod.ts?s=Option) are separated from
prototype.

## Feature

The [pipeline operator](https://github.com/tc39/proposal-pipeline-operator) will
linearize the nesting.

```ts, ignore
import { map, type Option, match } from "https://deno.land/x/optio/mod.ts";

declare const option: Option<unknown>;
declare const mapper: (value: unknown) => unknown

const result = map(option, mapper)
  |> map(%, mapper)
  |> match(%, {
    Some: mapper,
    None:mapper
  })
```

[proposal extensions](https://github.com/tc39/proposal-extensions) allows for
successive function adaptations, as in the Fluent API.

```ts, ignore
import { map, type Option, match } from "https://deno.land/x/optio/mod.ts";

declare const option: Option<unknown>;
declare const mapper: (value: unknown) => unknown

const result = option
  ::map(mapper)
  ::map(mapper)
  ::match({
    Some: mapper,
    None: mapper
  })
```

## API

See [deno doc](https://deno.land/x/optio?doc) for all APIs.

## Acknowledgements

- [Rust std::option](https://doc.rust-lang.org/std/option/index.html)

## Contributing

See [contribution](CONTRIBUTING.md).

## License

[MIT](LICENSE) © 2023 Tomoki Miyauchi
