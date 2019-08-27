# IOS

We currently support translating iOS apps, which store translations in .strings and .stringsdict files.

## Sign Up

Before you start translating, you'll need to [sign up for an account](https://www.langapi.co/signup).

## Install the CLI and login

> In the terminal, install the "langapi" node module globally.

```shell--all
#!/usr/bin/bash

> npm install -g langapi
> langapi login
```

To make it easy to translate apps via terminal, we've built our own command-line interface (CLI). Our CLI includes three main commands: **init, push, and pull**.

- init - Initializes langapi in a project folder
- push - Pushes translation requests to our server
- pull - Fetches completed translations

To get help on these commands, add the --help flag.

## Initialize

> To initialize langapi, run langapi init in the root directory of your ios repository

```shell-all
> langapi init
```

Run **langapi init** in your project's root directory. We will automatically detect your platform as iOS, and auto-generate some files, including a langapiconfig.json configuration file.

The **init** command may detect existing translations if you've already localized some files. Please only choose to load these into Lang if they are high-quality translations. We will internally mark them as human translations, and won't request any new translations unless the English strings change.

## Mark Localizable files

Before Lang can detect which strings to translate and which languages to translate to, you'll need to localize your project in Xcode.

1. Turn on Base Internationalization:

![alt text](https://raw.githubusercontent.com/PeterLZhou/slate/master/source/images/ios_base_internationalization.png "Logo Title Text 1")

2. Add target languages to Xcode

![alt text](https://raw.githubusercontent.com/PeterLZhou/slate/master/source/images/ios_add_language.png "Logo Title Text 1")

3. Localize your .strings and .stringsdict files for each language

Lang can only detected files explicitly for localization. For each .strings/.stringsdict file, open the right sidebar and click "Localize...", and check all the languages you want to translate to.

![alt text](https://raw.githubusercontent.com/PeterLZhou/slate/master/source/images/ios_localize_strings.png "Logo Title Text 1")

## Request translations

> To push translation requests, use 'langapi push'

```shell-all
> langapi push
```

Run **langapi push**, and we'll parse all your .strings/.stringsdict files for untranslated content, and request machine translations for them. To request human translations, run **langapi push --human**.

## Receive completed translations

> To pull in translation requests, use 'langapi pull'

```shell-all
> langapi pull
```

Run **langapi pull**, and we'll gather all of your finished translations and inject them into your .strings/.stringsdict files.

## Finish

That's it! To test and see the the translations, edit your build scheme, and change the language/region settings to your localized language. If you have any questions or if any of the steps above aren't working, please just email eric@langapi.co and we'll respond quickly :)
