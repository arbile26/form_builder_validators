# Form Builder Validators

Form Builder Validators set of validators for any `FormField` widget or widgets that extend the `FormField` class - *e.g.*, `TextFormField`, `DropdownFormField`, *et cetera*. It provides standard ready-made validation rules and a way to compose new validation rules combining multiple rules, including custom ones.

Also included is the `l10n` / `i18n` of error text messages to multiple languages.

[![Pub Version](https://img.shields.io/pub/v/form_builder_validators?logo=flutter&style=for-the-badge)](https://pub.dev/packages/form_builder_validators)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/flutter-form-builder-ecosystem/form_builder_validators/base.yaml?branch=main&logo=github&style=for-the-badge)](https://github.com/flutter-form-builder-ecosystem/form_builder_validators/actions/workflows/base.yaml)
[![Codecov](https://img.shields.io/codecov/c/github/flutter-form-builder-ecosystem/form_builder_validators?logo=codecov&style=for-the-badge)](https://codecov.io/gh/flutter-form-builder-ecosystem/form_builder_validators/)
[![CodeFactor Grade](https://img.shields.io/codefactor/grade/github/flutter-form-builder-ecosystem/form_builder_validators?logo=codefactor&style=for-the-badge)](https://www.codefactor.io/repository/github/flutter-form-builder-ecosystem/form_builder_validators)
---

> ## Migrating from version 7 to 8
>
> To migrate from v7 to v8, remove `context` as a parameter to validator functions. For example, `FormBuilderValidators.required(context)` becomes `FormBuilderValidators.required()` without `context` passed in.

## Contents

- [Features](#features)
- [Validators](#validators)
    - [Supported languages](#supported-languages)
- [Use](#use)
    - [Setup](#setup)
    - [Basic use](#basic-use)
    - [Specific uses](#specific-uses)
        - [Composing multiple validators](#composing-multiple-validators)
        - [Modify the default error message in a specific language](#modify-the-default-error-message-in-a-specific-language)
- [Support](#support)
    - [Contribute](#contribute)
        - [Add new supported language](#add-new-supported-language)
        - [Add new validator](#add-new-validator)
    - [Questions and answers](#questions-and-answers)
    - [Donations](#donations)
- [Roadmap](#roadmap)
- [Ecosystem](#ecosystem)
- [Thanks to](#thanks-to)

## Features

- Ready-made validation rules
- Compose multiple reusable validation rules
- Default error messages in multiple languages

## Validators

This package comes with several most common `FormFieldValidator`s such as required, numeric, mail,
URL, min, max, minLength, maxLength, minWordsCount, maxWordsCount, IP, credit card, etc., with default `errorText` messages.

Available built-in helper validators:

- `FormBuilderValidators.compose()` - runs each validator against the value provided.
- `FormBuilderValidators.conditional()` - conditionally runs a validator against the value provided.
- `FormBuilderValidators.or()` - runs each validator against the value provided and passes when any works.
- `FormBuilderValidators.transform()` - transforms the value before running the validator.
- `FormBuilderValidators.aggregate()` - runs the validators in parallel, collecting all errors.
- `FormBuilderValidators.log()` - runs the validator and logs the value at a specific point in the validation chain.
- `FormBuilderValidators.skipWhen()` - runs the validator and skips the validation when a certain condition is met.
- `FormBuilderValidators.defaultValue()` - runs the validator using the default value when the provided value is null.

Available built-in type validators include:

- `FormBuilderValidators.equal()` - requires the field's value to be equal to the provided object.
- `FormBuilderValidators.integer()` - requires the field's value to be an integer.
- `FormBuilderValidators.dateString()` - requires the field's value to be a valid date string.
- `FormBuilderValidators.dateTime()` - requires the field's value to be a valid date time.
- `FormBuilderValidators.dateRange()` - requires the field's value to be a within a date range.
- `FormBuilderValidators.time()` - requires the field's value to be a valid time string.
- `FormBuilderValidators.match()` - requires the field's value to match the provided regex pattern.
- `FormBuilderValidators.notMatch()` - requires the field's value to not match the provided regex pattern.
- `FormBuilderValidators.max()` - requires the field's value to be less than or equal to the provided number.
- `FormBuilderValidators.maxLength()` - requires the length of the field's value to be less than or equal to the provided maximum size.
- `FormBuilderValidators.maxWordsCount()` - requires the word count of the field's value to be less than or equal to the provided maximum count.
- `FormBuilderValidators.min()` - requires the field's value to be greater than or equal to the provided number.
- `FormBuilderValidators.minLength()` - requires the length of the field's value to be greater than or equal to the provided minimum length.
- `FormBuilderValidators.minWordsCount()` - requires the word count of the field's value to be greater than or equal to the provided minimum count.
- `FormBuilderValidators.equalLength()` - requires the length of the field's value to be equal to the provided minimum length.
- `FormBuilderValidators.numeric()` - requires the field's value to be a valid number.
- `FormBuilderValidators.required()` - requires the field to have a non-empty value.
- `FormBuilderValidators.uppercase()` - requires the field's value to be uppercase.
- `FormBuilderValidators.lowercase()` - requires the field's value to be lowercase.
- `FormBuilderValidators.isTrue()` - requires the field's to be true.
- `FormBuilderValidators.isFalse()` - requires the field's to be false.
- `FormBuilderValidators.hasSpecialChars()` - requires the field's to contain a specified number of special characters.
- `FormBuilderValidators.hasUppercaseChars()` - requires the field's to contain a specified number of uppercase characters.
- `FormBuilderValidators.hasLowercaseChars()` - requires the field's to contain a specified number of lowercase characters.
- `FormBuilderValidators.hasNumericChars()` - requires the field's to contain a specified number of numeric characters.
- `FormBuilderValidators.alphabetical()` - requires the field's to contain only alphabetical characters.
- `FormBuilderValidators.oddNumber()` - requires the field's to be an odd number.
- `FormBuilderValidators.evenNumber()` - requires the field's to be an even number.
- `FormBuilderValidators.between()` - requires the field's to be between two numbers.
- `FormBuilderValidators.containsElement()` - requires the field's to be in the provided list.
- `FormBuilderValidators.unique()` - requires the field's to be unique in the provided list.
- `FormBuilderValidators.singleLine()` - requires the field's string to be a single line of text.

Available built-in use-case validators include:

- `FormBuilderValidators.creditCard()` - requires the field's value to be a valid credit card number.
- `FormBuilderValidators.creditCardExpirationDate()` - requires the field's value to be a valid credit card expiration date and can check if not expired yet.
- `FormBuilderValidators.creditCardCVC()` - requires the field's value to be a valid credit card CVC number.
- `FormBuilderValidators.colorCode()` - requires the field's value to be a valid color code.
- `FormBuilderValidators.email()` - requires the field's value to be a valid email address.
- `FormBuilderValidators.ip()` - requires the field's value to be a valid IP address.
- `FormBuilderValidators.url()` - requires the field's value to be a valid URL.
- `FormBuilderValidators.fileExtension()` - requires the field's value to a valid file extension.
- `FormBuilderValidators.fileSize()` - requires the field's to be less than the max size.
- `FormBuilderValidators.password()` - requires the field's to be a valid password that matched required conditions.
- `FormBuilderValidators.uuid()` - requires the field's to be a valid uuid.
- `FormBuilderValidators.json()` - requires the field's to be a valid json string.
- `FormBuilderValidators.latitude()` - requires the field's to be a valid latitude.
- `FormBuilderValidators.longitude()` - requires the field's to be a valid longitude.
- `FormBuilderValidators.base64()` - requires the field's to be a valid base64 string.
- `FormBuilderValidators.path()` - requires the field's to be a valid file or folder path.
- `FormBuilderValidators.portNumber()` - requires the field's to be an valid port number.
- `FormBuilderValidators.macAddress()` - requires the field's to be an valid MAC address.
- `FormBuilderValidators.iban()` - requires the field's to be an valid IBAN.
- `FormBuilderValidators.bic()` - requires the field's to be an valid BIC.
- `FormBuilderValidators.isbn()` - requires the field's to be an valid ISBN.

Available extension methods used for chaining validators:

- `FormBuilderValidator.and()` - Combines the current validator with another validator using logical AND.
- `FormBuilderValidator.or()` - Combines the current validator with another validator using logical OR.
- `FormBuilderValidator.not()` - Negates the current validator.
- `FormBuilderValidator.when()` - Adds a condition to apply the validator only if the condition is met.
- `FormBuilderValidator.unless()` - Adds a condition to apply the validator only if the condition is not met.
- `FormBuilderValidator.transform()` - Transforms the value before applying the validator.
- `FormBuilderValidator.skipWhen()` - Skips the validator if the condition is met.
- `FormBuilderValidator.log()` - Logs the value during the validation process.
- `FormBuilderValidator.withMessage()` - Overrides the error message of the current validator.

### Supported languages

Validators support default `errorText` messages in these languages:

- Albanian (al)
- Arabic (ar)
- Bangla (bn)
- Bosnian (bs)
- Bulgarian (bg)
- Catalan (ca)
- Chinese Simplified (zh_Hans)
- Chinese Traditional (zh_Hant)
- Croatian (hr)
- Czech (cs)
- Danish (da)
- Dutch (nl)
- English (en)
- Estonian (et)
- Finnish (fi)
- Farsi/Persian (fa)
- French (fr)
- German (de)
- Greek (el)
- Hebrew (he)
- Hungarian (hu)
- Indonesian (id)
- Italian (it)
- Japanese (ja)
- Kurdish (ku)
- Korean (ko)
- Khmer (km)
- Lao (lo)
- Malay (ms)
- Mongolian (mn)
- Norwegian (no)
- Polish (pl)
- Portuguese (pt)
- Romanian (ro)
- Russian (ru)
- Slovak (sk)
- Slovenian (sl)
- Spanish (es)
- Swahili (sw)
- Swedish (se)
- Tamil(ta)
- Thai (th)
- Turkish (tr)
- Ukrainian (uk)
- Vietnamese (vi)

And you can still add your custom error messages.

## Use

### Setup

The default error message is in English. To allow for localization of default error messages within your app, add `FormBuilderLocalizations.delegate` in the list of your app's `localizationsDelegates`.

```Dart
return MaterialApp(
    supportedLocales: [
        Locale('de'),
        Locale('en'),
        Locale('es'),
        Locale('fr'),
        Locale('it'),
        ...
    ],
    localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        FormBuilderLocalizations.delegate,
    ],
```

### Basic use

```Dart
TextFormField(
    decoration: InputDecoration(labelText: 'Name'),
    autovalidateMode: AutovalidateMode.always,
    validator: FormBuilderValidators.required(),
),
```

See [pub.dev example tab](https://pub.dev/packages/form_builder_validators/example) or [github code](example/lib/main.dart) for more details

### Specific uses

#### Composing multiple validators

The `FormBuilderValidators` class comes with a handy static function named `compose()`, which takes a list of `FormFieldValidator` functions. Composing allows you to create once and reuse validation rules across multiple fields, widgets, or apps.

On validation, each validator is run, and if any validator returns a non-null value (i.e., a String), validation fails, and the `errorText` for the field is set as the returned string.

Example:

```Dart
TextFormField(
    decoration: InputDecoration(labelText: 'Age'),
    keyboardType: TextInputType.number,
    autovalidateMode: AutovalidateMode.always,
    validator: FormBuilderValidators.compose([
        /// Makes this field required
        FormBuilderValidators.required(),
        
        /// Ensures the value entered is numeric - with a custom error message
        FormBuilderValidators.numeric(errorText: 'La edad debe ser numérica.'),
        
        /// Sets a maximum value of 70
        FormBuilderValidators.max(70),
        
        /// Include your own custom `FormFieldValidator` function, if you want
        /// Ensures positive values only. We could also have used `FormBuilderValidators.min(0)` instead
        (val) {
            final number = int.tryParse(val);
            if (number == null) return null;
            if (number < 0) return 'We cannot have a negative age';
            return null;
        },
    ]),
),
```

#### Modify the default error message in a specific language

see [override_form_builder_localizations_en](example/lib/override_form_builder_localizations_en.dart) for more detail.

## Support

### Contribute

You have some ways to contribute to this package.

- Beginner: Reporting bugs or requesting new features
- Intermediate: Answer questions, implement new features (from issues or not), and create pull requests
- Advanced: Join [organization](#ecosystem) like a member and help to code, manage issues, discuss new features, and other things

See the [contribution file](https://github.com/flutter-form-builder-ecosystem/.github/blob/main/CONTRIBUTING.md) for more details

#### Add new supported language

We welcome efforts to internationalize/localize the package by translating the default validation `errorText` strings for built-in validation rules.

1. Add ARB files

    Create one ARB file inside the `lib/l10n` folder for each locale you need to add support. Name the files in the following way: `intl_<LOCALE_ISO_CODE>.arb`. For example: `intl_fr.arb` or `intl_fr_FR.arb`.

2. Translate the error messages

    Copy and paste the contents of `intl_en.arb` into your newly created ARB file. Then translate the error messages by overwriting the default messages.

3. Generate localization code

    To generate boilerplate code for localization, run the generate command inside the package directory where `pubspec.yaml` file is located:

    `flutter gen-l10n`

    The command will automatically create/update files inside the `lib/localization` directory, including your newly added locale support. The files in here are only necessary for local development and will not be committed to Github.

4. Update README

    Remember to update README, adding the new language (and language code) under [Supported languages section](#supported-languages) in alphabetic order, so that everyone knows your new language is now supported!

5. Submit PR

    Submit your PR and be of help to millions of developers all over the world!

#### Add new validator

1. Add method to `validators.dart` with your Dart documentation
2. Implement tests
3. Add to [validators](#validators) with name and description
4. Add message error translated on all languages (yes, all languages). To accomplish this need:
   a. Add property to all `intl_*.arb` files, in alphabetic order.
   b. Translate message in all languages.
   c. Run `flutter gen-l10n` command
5. Submit PR

### Questions and answers

You can ask questions or search for answers on [Github discussion](https://github.com/flutter-form-builder-ecosystem/form_builder_validators/discussions) or on [StackOverflow](https://stackoverflow.com/questions/tagged/flutter-form-builder)

### Donations

Donate or become a sponsor of Flutter Form Builder Ecosystem

[![Become a Sponsor](https://opencollective.com/flutter-form-builder-ecosystem/tiers/sponsor.svg?avatarHeight=56)](https://opencollective.com/flutter-form-builder-ecosystem)

## Roadmap

- [Solve open issues](https://github.com/flutter-form-builder-ecosystem/form_builder_validators/issues), [prioritizing bugs](https://github.com/flutter-form-builder-ecosystem/form_builder_validators/labels/bug)

## Ecosystem

Take a look at [our fantastic ecosystem](https://github.com/flutter-form-builder-ecosystem) and all packages in there

## Thanks to

[All contributors](https://github.com/flutter-form-builder-ecosystem/form_builder_validators/graphs/contributors)