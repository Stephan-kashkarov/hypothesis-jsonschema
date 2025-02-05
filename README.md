# hypothesis-jsonschema

A [Hypothesis](https://hypothesis.readthedocs.io) strategy for generating data
that matches some [JSON schema](https://json-schema.org/).

[Here's the PyPI page.](https://pypi.org/project/hypothesis-jsonschema/)

## API

The public API consists of just one function: `hypothesis_jsonschema.from_schema`,
which takes a JSON schema and returns a strategy for allowed JSON objects.

Schema reuse with "definitions" and "$ref" is not yet supported, but everything
else in drafts 04, 05, and 07 is fully tested and working.

For details on how to use this strategy in your tests,
[see the Hypothesis docs](https://hypothesis.readthedocs.io/).


## Supported versions

`hypothesis-jsonschema` does not support Python 2, because
[it's close to end of life](https://pythonclock.org/) and Python 3.6+ is a
much nicer language.  Contact me if you would like this changed and are
willing to either pay for or do the work to support Python 2.

In general, 0.x versions will require very recent versions of all dependencies
because I don't want to deal with compatibility workarounds.

`hypothesis-jsonschema` may make backwards-incompatible changes at any time
before version 1.x - that's what semver means! - but I've kept the API surface
small enough that this should be avoidable.  The main source of breaks will be
if or when schema that never really worked turn into explicit errors instead
of generating values that don't quite match.

Professional support for Hypothesis and hypothesis-jsonschema
is available as part of the [Tidelift Subscription][sub_link].
Tidelift gives software development teams a single source for purchasing and
maintaining their software, with professional grade assurances from the experts
who know it best.

[sub_link]: https://tidelift.com/subscription/pkg/pypi-hypothesis-jsonschema?utm_source=pypi-hypothesis-jsonschema&utm_medium=referral&utm_campaign=readme


### Changelog:

#### 0.9.6 - 2019-08-02
- A performance optimisation for null and boolean schema,
  which relies on a bugfix in `jsonschema >= 3.0.2`.

#### 0.9.5 - 2019-08-02
- Improved handling of the `contains` keyword for arrays

#### 0.9.4 - 2019-07-01
- Improved canonicalisation and merging for a wide range of schemas,
  which as usual unlocks significant optimisations and performance
  improvements for cases where they apply.

#### 0.9.3 - 2019-06-13
- Future-proofed canonicalisation of `type` key.

#### 0.9.2 - 2019-05-23
- Better internal canonicalization, which makes current and future
  optimisations more widely applicable.
- Yet another fix, this time for negative zero and numeric bouds as floats
  with sub-integer precision.  IEEE 754 is *tricky*, even with Hypothesis!
- Fixes handling of `enum` with elements disallowed by base schema,
  handling of `if-then-else` with a base schema, and handling of regex
  patterns that are invalid in Python.

#### 0.9.1 - 2019-05-22
- Fix the fix for numeric schemas with `multipleOf` and exclusive bounds.

#### 0.9.0 - 2019-05-21
- Supports merging schemas for overlapping `patternProperties`,
  a significant performance improvement in most cases.
- If the `"type"` key is missing, it is now inferred from other keys
  rather than always defaulting to `"object"`.
- Fixed handling of complicated numeric bounds.

#### 0.8.2 - 2019-05-21
- Improve performance for object schemas where the min and max size can be
  further constrained from `properties` and `propertyNames` attributes.

#### 0.8.1 - 2019-03-24
- Supports draft-04 schemata with the latest version of `jsonschema`

#### 0.8.0 - 2019-03-23
- Further improved support for `allOf`, `oneOf`, and `anyOf` with base schemata
- Added support for `dependencies`
- Handles overlapping `patternProperties`

#### 0.7.0 - 2019-03-21
- Now requires `jsonschema` >= 3.0
- Improved support for `allOf`, `oneOf`, and `propertyNames`
- Supports schemata with `"type": [an array of types]`
- Warning-free on Hypothesis 4.11

#### 0.6.1 - 2019-02-23
- Fix continuous delivery configuration (*before* the latent bug manifested)

#### 0.6.0 - 2019-02-23
- Support for conditional subschemata, i.e. the `if`, `then`, `else` keywords,
  and the `anyOf`, `allOf`, `oneOf`, and `not` keywords.

#### 0.5.0 - 2019-02-22
- Works with `jsonschema` 3.0 pre-release
- Initial support for draft06 and draft07

#### 0.4.2 - 2019-02-14
- Dropped dependency on `canonicaljson`
- Less warnings on Python 3.7

#### 0.4.1 - 2019-02-06
- Relicensed under the more permissive Mozilla Public License, like Hypothesis
- Requires Hypothesis version 4.0 or later
- Fixed an array bounds bug with `maxItems` and `contains` keywords

#### 0.4.0 - 2018-11-25
Supports string formats (email, datetime, etc) and simple use of the
`"contains"` keyword for arrays.

#### 0.3.0 - 2018-11-25
Good support for all basic types.  MVP.

#### 0.2.0 - 2018-11-24
Inference for null, boolean, string, and numeric types.

#### 0.1.0 - 2018-11-21
Stake in the ground (generate arbitrary JSON and filter it!)


### Security contact information
To report a security vulnerability, please use the
[Tidelift security contact](https://tidelift.com/security).
Tidelift will coordinate the fix and disclosure.
