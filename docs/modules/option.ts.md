---
title: option.ts
nav_order: 23
parent: Modules
---

# option overview

Added in v0.5.0

---

<h2 class="text-delta">Table of contents</h2>

- [OptionC (interface)](#optionc-interface)
- [NoneOutput (type alias)](#noneoutput-type-alias)
- [OptionOutput (type alias)](#optionoutput-type-alias)
- [SomeOutput (type alias)](#someoutput-type-alias)
- [option](#option)

---

# OptionC (interface)

Given a codec representing a type `A`, returns a codec representing `Option<A>` that is able to deserialize
the JSON representation of an `Option`.

**Signature**

```ts
export interface OptionC<C extends t.Mixed> extends t.Type<Option<t.TypeOf<C>>, OptionOutput<t.OutputOf<C>>, unknown> {}
```

**Example**

```ts
import { option } from 'io-ts-types/lib/option'
import { right } from 'fp-ts/lib/Either'
import { none, some } from 'fp-ts/lib/Option'
import * as t from 'io-ts'
import { PathReporter } from 'io-ts/lib/PathReporter'

const T = option(t.number)

assert.deepStrictEqual(T.decode(none), right(none))
assert.deepStrictEqual(T.decode(some(1)), right(some(1)))
assert.deepStrictEqual(PathReporter.report(T.decode(some('a'))), [
  'Invalid value "a" supplied to : Option<number>/1: Some<number>/value: number'
])
```

Added in v0.5.0

# NoneOutput (type alias)

**Signature**

```ts
export type NoneOutput = t.OutputOf<typeof None>
```

Added in v0.5.18

# OptionOutput (type alias)

**Signature**

```ts
export type OptionOutput<A> = NoneOutput | SomeOutput<A>
```

Added in v0.5.18

# SomeOutput (type alias)

**Signature**

```ts
export type SomeOutput<A> = { _tag: 'Some'; value: A }
```

Added in v0.5.18

# option

**Signature**

```ts
export function option<C extends t.Mixed>(codec: C, name: string = `Option<${codec.name}>`): OptionC<C> { ... }
```

Added in v0.5.0
