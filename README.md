# SalesTim Internationalization (i18n)

## Usage

I18n in SalesTim is implemented as a single json file for each language/region pair.

### Fallbacks
SalesTim takes care of fallback, such as:
- Language without region: ```en``` -> ```en-us```
- Region to region: ```en-en``` -> ```en-us```
- Language to language: ```zh-cn``` -> ```en-us```

To determine the language to be used, SalesTim is using these information by descending priority:
1. Microsoft Teams language
2. Client / Browser language
3. ``` en-us ``` in last resort

In addition to regular text, individual strings could use the following features:
- HTML (For some specific keys)
- Emojis
- Variables
- Plurals

### Variables

Strings may contain variables following the [printf notation](https://en.wikipedia.org/wiki/Printf_format_string), for instance:
``` json
{
  "alphabet": "The first 4 letters of the english alphabet are: %s, %s, %s and %s"
}
```

### Plurals

The following keys are supported in strings to handle multiple versions on the same message:
* zero
* one
* many

For instance:
``` json
{
  "enabled": {
    "zero": "Enabled with no approvers defined",
    "one": "Enabled for 1 approver",
    "many": "Enabled for %s approvers"
  }
}
```

## Implementation

SalesTim implements i18n using the following modules:
- Server-side: [i18n Module](https://www.npmjs.com/package/i18n)
- Client-side: [browser-i18n](https://www.npmjs.com/package/browser-i18n)

N.B: Client-side implementation is customized to implement the following capabilities:
- [JS Object Notation](https://en.wikipedia.org/wiki/JSON) for keys.
- Printf notation for strings implemented using the [sprintf-js](https://www.npmjs.com/package/sprintf-js) module.
