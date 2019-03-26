---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - typescript
  - python

toc_footers:
  - <a href='https://www.langapi.co'>Sign Up for Lang API</a>

search: true
---

# Introduction

LangAPI exists to help developers rapidly translate and localize their apps for users worldwide. We automate translation between a huge number of languages, including Spanish, French, Chinese, and Russian. To make the developer experience as smoooth as possible, translating a string is as simple as wrapping it with a special function. Currently, we only support JavaScript and TypeScript codebases. You can choose to either use machine translations (Google Translate) for testing, or human translations for production.

# Getting Started

Follow the steps below to translate your first string in under 3 minutes!

**NOTE:** This guide works for apps that do NOT use server-side rendering (SSR). To translate your SSR app, see [the getting started guide for SSR](#getting-started-ssr)

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

## Initialization

> To create a brand-new project, use Create React App

```shell-all
npm install -g create-react-app
create-react-app sample_project
cd sample_project
```

We'll need an existing codebase to translate in this step. Feel free to use your personal blog or sideproject repo. If you don't have a project handy, you can create one with [Create React App (CRA)](https://facebook.github.io/create-react-app/).

> To initialize langapi, run langapi init in the root directory and specify your source directory with the --src flag. Add --ts if you're using TypeScript, or --python if you're using Python.

```shell-all
> langapi init --src src
```

Run **langapi init --src <SOURCE_DIRECTORY>** inside the project's **root directory** and follow the instructions.

**NOTE: The source directory should be where your actual code is. It is usually different than the root directory**.

We recommend using machine translations for testing out the workflow.

## Configuring target languages

> The langapiconfig.json contains your LangApi settings for the current project.
> Here, we've added Chinese (zh) as a target language for demonstration.

```json--all
{
  "originalLanguage": "en",
  "targetLanguages": ["zh"]
}
```

After running **langapi init**, a new file **langapiconfig.json** will appear in your root directory. You can configure the behavior of LangAPI here, and you should check this file into your repository.

First, we'll need to set some target languages. To do this, open **langapiconfig.json** in any code editor, and in the targetLanguages property, add a comma-separated list of language encodings you want to translate to. By default, the original language is set to English (en).

[You can find a list of language encodings we support here](#language-codes).

## Mark string for translation

> We're using the App.js file in the src directory of our create-react-app

```javascript
import React, { Component } from "react";
// Make sure to import tr from your LangClient
import { tr } from "./langapi/LangClient";

class App extends Component {
  render() {
    return (
      <div>
        {/* Note the use of the tr function here */}
        Watch us translate: {tr("Hello world!")}
      </div>
    );
  }
}
```

```typescript
import React, { Component } from "react";
// Make sure to import tr from your LangClient
import { tr } from "./langapi/LangClient";

type Props = {};
type State = {};

class App extends Component<Props, State> {
  render() {
    return (
      <div>
        {/* Note the use of the tr function here */}
        Watch us translate: {tr("Hello world!")}
      </div>
    );
  }
}
```

```python
from LangClient import tr, param

def some_function(original_string, language):
    translated_string = tr(original_string, language)
```

To wrap a string for translation, import the **tr** function from the newly generated LangClient file in your source directory. We demonstrate this using the sample create-react-app project we created previously.

## Push and Pull Translations

> To push translation requests, use 'langapi push'

```shell-all
> langapi push
```

> To pull completed translations, use 'langapi pull'

```shell-all
> langapi pull
```

You're almost there! We've marked the string for translation, but we need to actually translate it. To push your un-translated strings to our server to be translated, run **langapi push** in your **root directory** (where langapiconfig.json is).

After the command is finished, you'll receive a breakdown of your strings to be translated.

Since we're using machine translations in this demo, the translations are done instantly! Thanks Google. To pull them back into your repo, run **langapi pull** in your **root directory**.

## Finish

Congratulations! You've just translated your first string using LangAPI. We hope it was easy enough, and we'd love to hear your feedback. Shoot one of us an email at eric@langapi.co or peter@langapi.co and let us know what you think!

# Getting Started (SSR)

Follow the steps below to translate your first string in under 3 minutes!

**NOTE:** This guide works for apps that use server-side rendering. Currently we **only support the NextJS framework.**

If you're not using SSR, see [the getting started guide for client-rendered applications](#getting-started).

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

## Initialization

> To create a brand-new project, use Create Next App

```shell-all
npm install -g create-next-app
create-next-app my-app
cd my-app
```

We'll need an existing codebase to translate in this step. Feel free to use your personal blog or sideproject repo. If you don't have a project handy, you can create one with [Create Next App (CRA)](https://open.segment.com/create-next-app/).

> To initialize langapi, run langapi init in the root directory and specify your source directory with the --src flag. Add --ts if you're using TypeScript.

```shell-all
> langapi init --src .
```

Run **langapi init --src <SOURCE_DIRECTORY>** inside the project's **root directory** and follow the instructions.

**NOTE: The source directory should be where your actual code is. In the example we're using the sample create-next-app, so the source directory is the same as the root directory.**.

We recommend using machine translations for testing out the workflow.

## Configuring target languages

> The langapiconfig.json contains your LangApi settings for the current project.
> Here, we've added Chinese (zh) as a target language for demonstration.

```json--all
{
  "originalLanguage": "en",
  "targetLanguages": ["zh"]
}
```

After running **langapi init**, a new file **langapiconfig.json** will appear in your root directory. You can configure the behavior of LangAPI here, and you should check this file into your repository.

First, we'll need to set some target languages. To do this, open **langapiconfig.json** in any code editor, and in the targetLanguages property, add a comma-separated list of language encodings you want to translate to. By default, the original language is set to English (en).

[You can find a list of language encodings we support here](#language-codes).

## Add withLang to components

```javascript
// in _app.js or _app.tsx
import React from "react";
import App, { Container } from "next/app";
import { withLang } from "langapi-client";
// If you're using TypeScript,
// add "resolveJsonModule": true to your tsconfig
import translations from "../langapi/translations.json";

class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props;

    return (
      <Container>
        <Component {...pageProps} />
      </Container>
    );
  }
}

export default withLang(translations, "YOUR_PUBLIC_KEY")(MyApp);
```

```typescript
// in _app.js or _app.tsx
import React from "react";
import App, { Container } from "next/app";
import { withLang, LangProps } from "langapi-client";
// If you're using TypeScript,
// add "resolveJsonModule": true to your tsconfig
import translations from "../langapi/translations.json";

type Props = {};
type State = {};

class MyApp extends App<Props, State> {
  render() {
    const { Component, pageProps } = this.props;

    return (
      <Container>
        <Component {...pageProps} />
      </Container>
    );
  }
}

export default withLang(translations, "YOUR_PUBLIC_KEY")(MyApp);
```

```python
# We don't support an equivalent for python yet - contact us at support@langapi,co if you want to see a supported framework!
```

To enable SSR translations, we provide a higher-order component (HOC) - **withLang** - that uses NextJS's **getInitialProps** function to load translations on the server.

We highly recommend wrapping your custom \_app with withLang to expose the 'tr' function to all of your server-side rendered components.

**NOTE:** Since we rely on getInitialProps, only components in the pages/ directory or other components that use getInitialProps will work with withLang. [See the NextJS documentation for details.](https://nextjs.org/docs/#imperatively-1)

## Mark string for translation

> withTranslation adds the tr function to components' props

```javascript
import * as React from "react";
import { withTranslation } from "langapi-client";

const Sample = props => {
  const { tr } = props;
  return (
    <div>
      <p>{tr("Hello world!")}</p>
    </div>
  );
};

export default withTranslation(Sample);
```

```typescript
import * as React from "react";
import { withTranslation, LangProps } from "langapi-client";

type InnerProps = {};
type Props = InnerProps & LangProps;

const Sample = (props: Props) => {
  const { tr } = props;
  return (
    <div>
      <p>{tr("Hello world!")}</p>
    </div>
  );
};

export default withTranslation<InnerProps>(Sample);
```

```python
# Nothing to see here ¯\_(ツ)_/¯
```

> You can also use React's new hook API.

```javascript
import * as React from "react";
import { useLang } from "langapi-client";

const Sample = props => {
  const { tr } = useLang();
  return (
    <div>
      <p>{tr("Hello world!")}</p>
    </div>
  );
};

export default Sample;
```

```typescript
import * as React from "react";
import { useLang } from "langapi-client";

type Props = {};

const Sample = (props: Props) => {
  const { tr } = useLang();
  return (
    <div>
      <p>{tr("Hello world!")}</p>
    </div>
  );
};

export default Sample;
```

```python
# I don't think there are React hooks in python.
```

To mark strings to be translated, we provide a **tr** function that you can wrap your strings with. The **tr** function automatically translates strings to the right language during runtime.

To wrap a string for translation, you have two choices:

- withTranslation higher-order component
- useLang hook

## Push and Pull Translations

> To push translation requests, use 'langapi push'

```shell-all
> langapi push
```

> To pull completed translations, use 'langapi pull'

```shell-all
> langapi pull
```

You're almost there! We've marked the string for translation, but we need to actually translate it. To push your un-translated strings to our server to be translated, run **langapi push** in your **root directory** (where langapiconfig.json is).

After the command is finished, you'll receive a breakdown of your strings to be translated.

Since we're using machine translations in this demo, the translations are done instantly! Thanks Google. To pull them back into your repo, run **langapi pull** in your **root directory**.

## Finish

Congratulations! You've just translated your first string using LangAPI. We hope it was easy enough, and we'd love to hear your feedback. Shoot one of us an email at eric@langapi.co or peter@langapi.co and let us know what you think!

# Lots of Legacy Code - Codegen (BETA)

If you have a lot of code to wrap with tr's, we provide a code generation tool that will run through your files and wrap all inferred front-facing strings. We currently support React only - ping us if you want a similar tool for your framework at support@langapi.co.

```shell-all
> langapi generate [directory]
```

# Interpolation

Interpolation allows you to add dynamic values to your translations, and will be escaped during the translation. You must put param() calls inside of tr() calls.

```javascript
// *.js, *.jsx
import { tr, param } from "./LangClient";

var ESCAPED_SITE = "Lang API";
var translatedString = tr("Welcome to " + param(ESCAPED_SITE) + "!");

// translatedString (es): ¡Bienvenido a Lang API!
```

```typescript
// *.ts, *.tsx
import { tr, param } from "./LangClient";

const ESCAPED_SITE = "Lang API";
const translatedString = tr("Welcome to " + param(ESCAPED_SITE) + "!");

// translatedString (es): ¡Bienvenido a Lang API!
```

```python
# *.py
from LangClient import tr, param

ESCAPED_SITE = "Lang API";
language = "es"
translated_string = tr("Welcome to " + param(ESCAPED_SITE) + "!", language);

# translated_string (es): ¡Bienvenido a Lang API!
```

#Language Codes

Here are the supported language codes you can use as originalLanguage and targetLanguages inside of langconfig.json.

| Code  | Language                |
| ----- | ----------------------- |
| fr-ca | French (Canada)         |
| da    | Danish                  |
| zh-tw | Chinese (Traditional)   |
| pt-br | Portuguese (Brazil)     |
| uk    | Ukrainian               |
| lt    | Lithuanian              |
| th    | Thai                    |
| dt    | Desktop                 |
| fi    | Finnish                 |
| ro    | Romanian                |
| is    | Icelandic               |
| es-la | Spanish (Latin America) |
| el    | Greek                   |
| hi    | Hindi                   |
| hu    | Hungarian               |
| fr    | French                  |
| it    | Italian                 |
| ko    | Korean                  |
| bg    | Bulgarian               |
| cs    | Czech                   |
| sk    | Slovak                  |
| pt    | Portuguese (Europe)     |
| en-gb | English (British)       |
| sv    | Swedish                 |
| id    | Indonesian              |
| de    | German                  |
| ms    | Malay                   |
| vi    | Vietnamese              |
| zh    | Chinese (Simplified)    |
| ge    | Generic                 |
| tl    | Tagalog                 |
| es    | Spanish (Spain)         |
| sr    | Serbian                 |
| ar    | Arabic                  |
| he    | Hebrew                  |
| nl    | Dutch                   |
| no    | Norwegian               |
| pl    | Polish                  |
| ja    | Japanese                |
| ru    | Russian                 |
| tr    | Turkish                 |
| en    | English                 |

If you want support for a language we don't have yet, reach out to us at support@langapi.co. We're always on call and happy to help!

# Changelog
