---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - typescript
  - python

toc_footers:
  - <a href='https://www.langapi.co'>Sign Up for Lang API</a>

search: true

includes:
  - ios
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

# Getting Started (SSR, NextJS only)

Follow the steps below to translate your first string in under 3 minutes!

**NOTE:** This guide is for apps that use server-side rendering. **Currently we only support the NextJS framework.**

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

We'll need an existing codebase to translate in this step. Feel free to use your personal blog or sideproject repo. If you don't have a project handy, you can create one with [Create Next App](https://open.segment.com/create-next-app/).

> To initialize langapi, run langapi init in the root directory and specify your source directory with the --src flag. Add --ts if you're using TypeScript.

```shell-all
> langapi init --src .
```

Run **langapi init --src <SOURCE_DIRECTORY>** inside the project's **root directory** and follow the instructions. Then, run **yarn add langapi-next** or **npm install --save langapi-next**. We need a special library to enable support for loading translations in the Next.js server.

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
import { withLang } from "langapi-next";
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

export default withLang("YOUR_PUBLIC_KEY", translations)(MyApp);
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

export default withLang("YOUR_PUBLIC_KEY", translations)(MyApp);
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
import { withTranslation } from "langapi-next";

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
import { withTranslation, LangProps } from "langapi-next";

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
import { useLang } from "langapi-next";

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

# LangClient

LangClient is the core module of Lang. It gets automatically installed during **langapi init**, and we generate some files for you so you don't have to configure it and can get started immediately. However, you can interact with its APIs directly, and we list them here:

## Initializing LangClient

```javascript
// *.js, *.jsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));
```

```typescript
// *.ts, *.tsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));
```

To initialize LangClient, we simply require() it and pass in the required arguments. The first argument is your Lang publishable key. The second argument is the JSON object from your translations.json file, which should be in your auto-generated langapi directory.

By default, LangClient attempts to detect the user's language automatically and translate to that language. This can be overridden, [see setLanguage.](##setLanguage)

## tr

```javascript
// *.js, *.jsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Tries to translate "Hello world!" into currently set language.
LangClient.tr("Hello world!")

// The second argument contains context variables for the string
LangClient.tr("Hello world, {name}!", {name: "Eric"});

// The third argument is a force language override
// Here, LangClient will try to translate to Spanish
LangClient.tr("Hello world, {name}!", {name: "Eric"}, "es");
```

```typescript
// *.ts, *.tsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Tries to translate "Hello world!" into currently set language.
LangClient.tr("Hello world!")

// The second argument contains context variables for the string
LangClient.tr("Hello world, {name}!", {name: "Eric"});

// The third argument is a force language override
// Here, LangClient will try to translate to Spanish
LangClient.tr("Hello world, {name}!", {name: "Eric"}, "es");
```

**tr** is the bread-and-butter of LangClient. It takes a string and two optional arguments, and attempts to translate the string using translations loaded in via translations.json. See the code sample for all argument possibilities.

## setForceLanguage

```javascript
// *.js, *.jsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Forces the language to Spanish
LangClient.setForceLanguage("es");
```

```typescript
// *.ts, *.tsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Forces the language to Spanish
LangClient.setForceLanguage("es");
```

**setForceLanguage** explictly tells LangClient to use a specific language code, overriding the default language LangClient detects from the user's browser. This is useful when you have options on your app to change a user's language settings and want to override the default.

## getLanguage

```javascript
// *.js, *.jsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Forces the language to Spanish
LangClient.setForceLanguage("es");
// Returns "es"
LangClient.getLanguage();
```

```typescript
// *.ts, *.tsx

const LangClient = require('langapi-client')("YOUR_PUBLISHABLE_KEY", require("./translations.json));

// Forces the language to Spanish
LangClient.setForceLanguage("es");
// Returns "es"
LangClient.getLanguage();
```

**getLanguage** fetches the current language LangClient is translating to. This is useful if you want to display the current language to users, or save it into your state/backend.

# Formatting Strings

We understand that most strings aren't just blocks of text. Here, we'll go through common examples of writing more complex strings, including ones that have variables and plural forms.

Our formatting follows the [ICU (International Components for Unicode) Message syntax](http://userguide.icu-project.org/formatparse/messages), an international standard.

Why do you need to format your strings? Not all languages have the same grammar, and it enables translators to easily understand all the components in your string and translate it to any language in the world.

## Variables

To mark the presence of a variable in a string, wrap the variable name with curly braces, and supply an object to the **tr** call that contains the variable's name and value.

**NOTE:** Unless the variable is a string constant that has been wrapped with **tr**, it will appear in its original form in the string. In the example, although the rest of the sentence has been translated to Spanish, the variable will display in its raw value.

```javascript
// *.js, *.jsx
import { tr } from "./LangClient";

var context = { sitename: "Lang API" };
var translatedString = tr("Welcome to {sitename}!", context);

// translatedString (Spanish): ¡Bienvenido a Lang API!
```

```typescript
// *.ts, *.tsx
import { tr } from "./LangClient";

var context = { sitename: "Lang API" };
const translatedString = tr("Welcome to {sitename}!", context);

// translatedString (es): ¡Bienvenido a Lang API!
```

```python
# *.py
from LangClient import tr, param

ESCAPED_SITE = "Lang API";
language = "es"
context = {sitename: "Lang API", targetLanguage: language }
translated_string = tr("Welcome to {sitename}!", context);

# translated_string (es): ¡Bienvenido a Lang API!
```

## Plurals

For strings that have plural forms, use the ICU pluralization syntax to ensure they are translated correctly in every plural form. With other libraries, you would write and translate multiple strings to account for all plural forms. With Lang, you can just write it once!

**NOTE:** There are certain languages with more than one plural form. Czech has three. Here's an example:

I have 1 apple => Mám 1 jablko.

I have 3 apples => Mám 3 jablka.

I have 10 apples => Mám 10 jablek.

**If you use the ICU syntax, there's nothing else you have to do. We'll handle all cases for you. Lang accounts for every plural form in every language.**

```javascript
// *.js, *.jsx
import { tr } from "./LangClient";

var translatedString = tr(
  `I have {count, plural, 
    =0 {no apples} 
    =1 {1 apple} 
    other {{count} apples}}.`,
  { count: 1 }
);

// translatedString (Spanish): Tengo 1 manzana.

var translatedString = tr(
  `I have {count, plural, 
    =0 {no apples} 
    =1 {1 apple} 
    other {{count} apples}}.`,
  { count: 7 }
);

// translatedString (Spanish): Tengo 7 manzanas.
```

```typescript
// *.ts, *.tsx
import { tr } from "./LangClient";

var translatedString = tr(
  `I have {count, plural, 
    =0 {no apples} 
    =1 {1 apple} 
    other {{count} apples}}.`,
  { count: 1 }
);

// translatedString (Spanish): Tengo 1 manzana.

var translatedString = tr(
  `I have {count, plural, 
    =0 {no apples} 
    =1 {1 apple} 
    other {{count} apples}}.`,
  { count: 7 }
);

// translatedString (Spanish): Tengo 7 manzanas.
```

```python
# *.py
from LangClient import tr

translatedString = tr(
  "I have {count, plural, =0 {no apples} =1 {1 apple} other {{count} apples}}.!",
  { count: 7, language: "es" }
);

// translatedString (es): ¡Tengo 7 manzanas!
```

## Select

Some sentences require different words depending on information like gender. You can show different phrases in a string that depend on the **value** of a variable by using "select".

```javascript
// *.js, *.jsx
import { tr } from "./LangClient";

// For the sake of simplicity, we are not listing all genders in this example.
var translatedString = tr(
  `{gender, select, 
    male {He likes} 
    female {She likes} 
    other {they like}} eating apples`,
  { gender: "female" }
);

// translatedString (Spanish): A ella le gusta comer manzanas.
```

```typescript
// *.ts, *.tsx
import { tr } from "./LangClient";

// For the sake of simplicity, we are not listing all genders in this example.
var translatedString = tr(
  `{gender, select, 
    male {He likes} 
    female {She likes} 
    other {they like}} eating apples`,
  { gender: "female" }
);

// translatedString (Spanish): A ella le gusta comer manzanas.
```

```python
# *.py
from LangClient import tr

translatedString = tr(
  "{gender, select,\
    male {He likes}\
    female {She likes}\
    other {they like}} eating apples",
  { count: 7, language: "es" }
);

// translatedString (Spanish): A ella le gusta comer manzanas.
```

## Codemod (EXPERIMENTAL)

If you have a lot of code to wrap with tr's, we provide a code generation tool that will run through your files and wrap all inferred front-facing strings. We currently support React only - ping us if you want a similar tool for your framework at support@langapi.co.

```shell-all
> langapi generate [directory]
```

# React

At Lang, we love and use React :)

Here we show the components we've built to make using Lang even easier. To use these components, run the command below in your project root:

**npm install --save react-langapi**

[Here's a link to the source code for the components.](https://github.com/cyrieu/react-langapi)

## LangProvider

```javascript
// Remember to run "npm install --save react-langapi"
// *.js, *.jsx

// At your top-level component (Usually App.js)

import { LangProvider } from "react-langapi";
// Relative path to auto-generated LangClient.js file
import { LangClient } from "./langapi/LangClient";

class RootApp extends React.Component {
  state = {
    currentLanguage: "en" // default
  };

  render() {
    // currentLanguage could be from any state
    const { currentLanguage } = this.state;
    return (
      <LangProvider client={LangClient} currentLanguage={currentLanguage}>
        <App /> {/* App will re-render when currentLanguage changes */}
      </LangProvider>
    );
  }
}

// On re-render, tr() will update to the newest currentLanguage
import { tr } from "./langapi/LangClient";
const App = () => <div>{tr("Hello world!")}</div>;
```

```typescript
// Remember to run "npm install --save react-langapi"
// *.ts, *.tsx

// At your top-level component (Usually App.js)

import { LangProvider } from "react-langapi";
// Relative path to auto-generated LangClient.js file
import { LangClient } from "./langapi/LangClient";

class RootApp extends React.Component {
  state = {
    currentLanguage: "en" // default
  };

  render() {
    // currentLanguage could be from any state
    const { currentLanguage } = this.state;
    return (
      <LangProvider client={LangClient} currentLanguage={currentLanguage}>
        <App /> {/* App will re-render when currentLanguage changes */}
      </LangProvider>
    );
  }
}

// On re-render, tr() will update to the newest currentLanguage
import { tr } from "./langapi/LangClient";
const App = () => <div>{tr("Hello world!")}</div>;
```

If a user decides to change their preferred language on the frontend, **LangClient** and **tr** won't know the new language unless you notify it. The React app also won 't re-render, because Lang is a standalone module and not connected to React's state. To solve these problems, we've built **LangProvider**, which let's you connect Lang with your app's state.

In our code example, we show a sample App component using LangProvider. We use React's basic State API to show how a change to currentLanguage will re-render the entire component tree, but you can pass in a stateful variable from your Redux or MobX stores as well.

## Tr

```javascript
// Remember to run "npm install --save react-langapi"
// *.js, *.jsx

// Inside a component wrapped by <LangProvider />
import React from "react";
import { Tr } from "react-langapi";

class ChildComponent extends React.Component {
  render() {
    return (
      <div>
        <Tr>Hello world!</Tr>
        <Tr variables={{ count: 5 }}>I have {"{count}"} apples</Tr>
      </div>
    );
  }
}
```

```typescript
// Remember to run "npm install --save react-langapi"
// *.js, *.jsx

// Inside a component wrapped by <LangProvider />
import React from "react";
import { Tr } from "react-langapi";

class ChildComponent extends React.Component {
  render() {
    return (
      <div>
        <Tr>Hello world!</Tr>
        <Tr variables={{ count: 5 }}>I have {"{count}"} apples</Tr>
      </div>
    );
  }
}
```

The Tr React component functions exactly like the tr function. Make sure to format the phrase inside in ICU format - to pass escaped variables in, supply them as a dictionary using the `variables` prop.

## Legacy Support

For versions of React that do not support the Context API (introduced in 16.3.0), you can still make use of the React bindings!

Just copy the code-snippet into LangClient and you can now import the Tr component througout your application.

```javascript
// Add into LangClient.js
import {TrLegacy, withLang} from 'react-langapi';

// named export 
export const Tr = withLang(TrLegacy, LangClient);
```

```typescript
// Add into LangClient.ts
import {TrLegacy, withLang} from 'react-langapi';

// named export 
export const Tr = withLang(TrLegacy, LangClient);
```

# Android

We have built a Gradle plugin for Android which makes it very simple to localize your app. Currently, the only requirement is that strings in the native language be located in a 'strings.xml' file.

## Install the Plugin

> Using the Groovy plugins DSL:

```groovy--all
plugins {
  id "co.langapi.langplugin" version "1.3"
}
```

> Using Groovy legacy plugin applications:

```groovy--all
buildscript {
  repositories {
    maven {
      url "https://plugins.gradle.org/m2/"
    }
  }
  dependencies {
    classpath "gradle.plugin.co.langapi:cli:1.3"
  }
}

apply plugin: "co.langapi.langplugin"
```

You can add the plugin by making a small modification to your build.gradle file. If your build files are in Kotlin, visit [official instructions](https://plugins.gradle.org/plugin/co.langapi.langplugin) for more details.

## Run initialize

First, sync gradle if your IDE hasn't already autosynced. Then in the root directory use the gradle wrapper to run the initialization task. 

```shell--all
#!/usr/bin/bash

> gradlew initialize
```

```json--all
{
  "originalLanguage": "en",
  "originalSourceFile": "path/to/strings.xml",
  "apiKey": "YOUR_API_KEY",
  "languages": [
    {
      "targetLanguage": "es",
      "targetSourceFile": "path/to/target/language/strings.xml"
    }
  ]
}
```

After running **gradlew initialize**, a new file **langapiconfig.json** will appear in your root directory. You can configure the behavior of Lang here, and you should check this file into version control.

The configuration file, langapiconfig.json, declares the path of the original strings.xml file and the new strings.xml files for each language.

We'll add Spanish as an example. You can find a list of language encodings we support [here](#language-codes).
You can find your API Key on the dashboard if you click on your project in the 'Projects' tab. If you haven't signed up for an account check out [getting started](#getting-started)

## Request translations

Now we're all set to request translations! Simply run **gradlew push** in your root directory. This will request **machine translations** so this will be available to pull instantly.

```shell--all
#!usr/bin/bash

> gradlew push
```

## Receive translations

To receive the translations, run **gradlew pull** in your root directory. Lang will save the translated xml files to the paths specified in your langapiconfig.json.

```shell--all
#!usr/bin/bash

> gradlew pull
```

Lang will pull the machine translation for phrases with no complete human translations. Translations are marked as 'Human' or 'Machine' as a comment in the translated strings.xml file.

```xml--all
<resources>
    <!--Translation type: Machine-->
    <string name="app_name">Mi aplicación</string>
    <!--Translation type: Human-->
    <string name="landing_text">Hola amigos</string>
</resources>
```

## Mark string for no translation
If you don't want a string to be translated, simply set a translatable attribute to false.

```xml--all
<!-- strings.xml-->
<resources>
    <string name="string-element" translatable="false">Don't translate this string element</string>
    <string-array name="array">
        <string name="array-element" translatable="false">Don't translate this array element</string>
    </string-array>
<resources>
```

## Upload existing translations

If you have existing translations in string.xml files then add them to the config as explained [here](#run-initialize). Then simply run **gradlew upload**. Be careful to only upload files with professional translations because all uploaded translations will be marked as 'Human'.

```shell--all
#!usr/bin/bash

> gradlew upload
```

# GatsbyJS

We've built a custom plugin for Gatsby, one of the most popular React-based static site generators, to make it easy to localize your app, personal page, or blog.

In this section, we assume you've created your own Gatsby project (if you haven't, [you can use the Gatsby CLI](https://www.gatsbyjs.org/docs/gatsby-cli/)).

## Install the CLI

> In the terminal, install the "langapi" node module globally.

```shell--all
#!/usr/bin/bash

> npm install -g langapi
# Run "langapi login" if you have an account.
> langapi login
# Run "langapi signup" if you don't.
> langapi signup
```

To start, you'll need to install the Lang command-line interface tool. See the docs on the CLI to understand the various commands and options.

## Run init

> To initialize langapi, run langapi init in the root directory and specify your source directory with the --src flag. Add --ts if you're using TypeScript.

```shell-all
#!/usr/bin/bash

# This command initializes lang, with "src" as the source directory
> langapi init src
```

Run **langapi init <YOUR_SOURCE_DIRECTORY>** inside the project's **root directory** and follow the instructions. The source directory should be where all of your code is stored. The root directory contains your package.json and other configuration files.

## Add your first language

> The langapiconfig.json contains your LangApi settings for the current project.
> Here, we've added Spanish (es) as a target language.

```json--all
{
  "src": "src",
  "originalLanguage": "en",
  "targetLanguages": ["es"]
}
```

After running **langapi init**, a new file **langapiconfig.json** will appear in your root directory. You can configure the behavior of Lang here, and you should check this file into your repository.

We'll add Spanish as an example. [You can find a list of language encodings we support here](#language-codes).

## Install gatsby-plugin-lang

```shell--all
#!/usr/bin/bash

> npm install --save gatsby-plugin-lang
```

Next, we'll need to install the Lang plugin for Gatsby in your project.

## Configure gatsy-config.js

```javascript
// *.js

module.exports = {
  siteMetadata: {
    title: `Gatsby Lang Demo`,
    description: `Get started with Lang!`,
    author: `@cyrieu`
  },
  plugins: [
    // .... Your existing plugins
    {
      resolve: `gatsby-plugin-lang`,
      options: {
        // The path to your generated langapi folder in your source directory
        path: `${__dirname}/src/langapi`,
        // Your targetLanguages, as defined in langapiconfig.json
        languages: ["es"],
        // Your originalLanguage, as defined in langapiconfig.json
        defaultLanguage: "en",
        // Set this to true if you want to automatically redirect
        // visitors to pages in their preferred language on your app
        redirect: true
      }
    }
    // this (optional) plugin enables Progressive Web App + Offline functionality
    // To learn more, visit: https://gatsby.dev/offline
    // `gatsby-plugin-offline`,
  ]
};
```

To get the plugin working, we need to add it to our gatsy-config.js. An example is shown here with all the options available.

**IMPORTANT** The "languages" option should be the same as the targetLanguages you've set in langapiconfig.json

## Wrap your first string

```javascript
// *.js, *.jsx
import React from "react";

import Layout from "../components/layout";
import { tr } from "../langapi/LangClient";
import { Tr, Link } from "gatsby-plugin-lang";

const IndexPage = props => {
  return (
    <Layout>
      <Tr>
        <h1>Your first translated string!</h1>
      </Tr>
      <Link to="/page-2/">Go to page 2</Link>
    </Layout>
  );
};

export default IndexPage;
```

That's it for configuration! Open up any component/page, and import { Tr } from "gatsby-plugin-lang". All of our React components are included with the Gatsby plugin. [You can read the React docs here.](#React)

**NOTE**: Notice the Link component we're using here is from the Lang plugin. We can't use the default Gatsby Link, because Lang automatically sets up separate subdomains for your different languages. For example, Spanish pages are located at "yourdomain.com/es". See [Routing for more details](##Routing).

## Finish

> To push translation requests, use 'langapi push'

```shell-all
> langapi push
```

> To pull completed translations, use 'langapi pull'

```shell-all
> langapi pull
```

> Then, run "gatsby develop" and navigate to localhost:8000/targetLanguageCode

```shell-all
> gatsby develop
```

Now, in your root directory, run "langapi push". Our CLI will find all the translation calls in your code and automatically request machine translations for them. Since they're machine translations, they're done immediately! Run "langapi pull" to store your translations inside your translations.json file. Finally, run "gatsby develop", navigate to localhost:8000/es or localhost:8000/ja, and check out your newly translated app!

## Routing

```javascript
// *.js, *.jsx
import React from "react";

import Layout from "../components/layout";
import { Link } from "gatsby-plugin-lang";

const IndexPage = props => {
  return (
    <Layout>
      {/* Our <Link /> component preserves the language routing in your app */}
      <Link to="/page-2/">Go to page 2</Link>
    </Layout>
  );
};

export default IndexPage;
```

Gatsby is a static site generator, and we hook into Gatsby's build process to automatically generate separate pages for each language you use in your app. If your target languages are Spanish (es) and Japanese (ja), we'll automatically create yourdomain.com/es and yourdomain.com/ja, which are the translated versions of your site in Spanish and Japanese respectively.

**IMPORTANT** You must use the Link component in "gatsby-plugin-lang" to perform navigation, otherwise a user will be sent from a Japanese version of the site (e.g. yourdomain.com/ja/home) to the English version (e.g. yourdomain.com/home).

## Hot Reloading

```javascript
// *.js, *.jsx
/**
 * Implement Gatsby's Browser APIs in this file.
 *
 * See: https://www.gatsbyjs.org/docs/browser-apis/
 */
const React = require("react");
const client = require("langapi-client")(
  "sk_prod_4505fd24-7157-4e06-b473-52481db18f6d", // Your publishable key. See https://www.langapi.co/dashboard
  require("./src/langapi/translations.json")
);
const { LangProvider } = require("gatsby-plugin-lang");

exports.wrapRootElement = ({ element }) => {
  return <LangProvider client={client}>{element}</LangProvider>;
};
```

Since our plugin builds the translated version of your app during the "gatsby-node.js" phase, your browser won't show the newest translations even if you "langapi pull" during "gatsby develop", since Gatsby only re-runs the code in "gatsby-ssr.js" and "gatsby-browser.js". We're still working on this, but here's a quick way to force your browser to reload your translations without re-running "gatsby develop" or "gatsby build".

Add the snippet of code to your "gatsby-browser.js" file. This will force Gatsby to re-inject your translation data into the app each time translations.json is updated. Now you can pull in new translations and your browser will automatically show them!

# Continuous Translation

Sites that have continuously generated content, like forums or user-generated content, need a way to translate on the fly. Lang has tools that make continuous translation super easy.

## LiveTr

```javascript
// Relative path to auto-generated LangClient.js file
import { liveTr } from "./langapi/LangClient";

function submitProductListing(productDescription) {
  // This requests a human translation for productDescription from English into Chinese and French.
  const translation = liveTr(productDescription, {
    requestTargetLanguages: ["zh"],
    lookupTargetLanguage: "zh",
    originalLanguage: "en",
    projects: ["test-project"],
    description: "This is a product listing",
    requestMachine: false
  });
}

// An example of requesting translations during a form submission
class Form extends React.Component {
  state = { productDescription: "" };

  handleChange = event => {
    this.setState({ value: event.target.value });
  };

  handleSubmit = event => {
    const translation = liveTr(this.state.productDescription, {
      requestTargetLanguages: ["zh"],
      lookupTargetLanguage: "zh",
      originalLanguage: "en",
      projects: ["test-project"],
      description: "This is a product listing",
      requestMachine: false
    });
  };
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          value={this.state.productDescription}
          onChange={this.handleChange}
        />
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

```typescript
// Relative path to auto-generated LangClient.js file
import { liveTr } from "./langapi/LangClient";

function submitProductListing(productDescription: string) {
  // This requests a human translation for productDescription from English into Chinese and French.
  const translation = liveTr(productDescription, {
    requestTargetLanguages: ["zh"],
    lookupTargetLanguage: "zh",
    originalLanguage: "en",
    projects: ["test-project"],
    description: "This is a product listing",
    requestMachine: false
  });
}

// An example of requesting translations during a form submission
type State = {
  productDescription: string;
};

class Form extends React.Component<{}, State> {
  state: State = { productDescription: "" };

  handleChange = event => {
    this.setState({ value: event.target.value });
  };

  handleSubmit = event => {
    const translation = liveTr(this.state.productDescription, {
      requestTargetLanguages: ["zh"],
      lookupTargetLanguage: "zh",
      originalLanguage: "en",
      projects: ["test-project"],
      description: "This is a product listing",
      requestMachine: false
    });
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          value={this.state.productDescription}
          onChange={this.handleChange}
        />
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

```python
from LangClient import liveTr

def submitProductListing(productDescription):
  # This requests a human translation for productDescription from English into Chinese and French.
  translation = liveTr(productDescription, {
    "requestTargetLanguages": ["zh"],
    "originalLanguage": "en"
    "projects": ["test-project"],
    "description": "This is a product listing",
    "requestMachine": False,
  })
```

**usage: liveTr(PHRASE, CONFIG)**

The liveTr function is exposed in the autogenerated LangClient. The function attempts to return a translation for PHRASE by doing a lookup inside of translations.json. If no translation is found, it will asynchronously attempt to return a translation from our server. If none is found, it will request a translation and fallback to the original phrase.

A common use case is to put the liveTr function inside of the pipeline where you are continuously sending phrases out to your users.

The arguments should have the following form:

- `phrase`: the string representing the phrase being translated.
- `config`: an object that should have the following keys:
  - `originalLanguage`: a string representing the language code of the original language.
  - `requestTargetLanguages`: an array of string language codes representing the target languages you want to translate the phrase into.
  - `lookupTargetLanguage`: a string representing the langauge code of the requested translation
  - `projects` (optional): an array of strings containing the project names you want to request and receive translations for. If you only own one project, this is optional. Otherwise, you must supply a project name.
  - `description` (optional): A human-readable string description of the content you are translating. This will be sent to the translator for context. If description is supplied, the phrase and description combination will also be used as a unique identifier for future lookups.
  - `requestMachine` (optional): Defaults to true. If set to false, human translations for the phrase will be requested, otherwise machine translations will be requested.
  - `pipeline` (optional): A string value representing what workflow you want your translations to go through. [Contact sales](mailto:sales@langapi.co) for information on how to customize translation workflows.

By default, all of our dynamic translations are hosted on our CDN. We have solutions for self-hosting as well as integrations with your own database instrastructure - [Contact sales](mailto:sales@langapi.co) for more information.

To avoid your users making additional network requests, it is recommended you lookup translations server-side before serving them to the client. Optionally, you can run `langapi pull --live` on the CLI to cache all continuous translations into your translations.json.

## API

```markdown
# cURL

cURL -X POST "https://lang-backend.herokuapp.com/api/v1/livetr" \
 -H 'Authorization: Token <Your API_KEY>' \
 -d phrase='I want this translated' \
 -d original_language='en' \
 -d request_target_language='es' \
 -d request_target_language='zh' \
 -d lookup_target_language='es' \
 -d pipeline='p0' \
 -d project='test-project' \
 -d request_machine=false \
 -d description='This is a description of the phrase'
```

> The above request returns a response like this:

```json
{
  "translation": "Quiero esto traducido",
  "status": "complete",
  "original_language": "en",
  "target_language": "es"
}
```

We offer an API endpoint that functions the same way as the liveTr function.

The arguments should have the following form:

- `phrase`: the string representing the phrase being translated.
- `originalLanguage`: a string representing the language code of the original language.
- `requestTargetLanguage`: a string representing the language code of the requested translated language. One argument should be provided for each requested language.
- `lookupTargetLanguage`: a string representing the langauge code of the requested translation
- `project` (optional): a string containing the project name you want to request and receive translations for. If you only own one project, this is optional. Otherwise, you must supply a project name.
- `description` (optional): A human-readable string description of the content you are translating. This will be sent to the translator for context. If description is supplied, the phrase and description combination will also be used as a unique identifier for future lookups.
- `requestMachine` (optional): Defaults to true. If set to false, human translations for the phrase will be requested, otherwise machine translations will be requested.
- `pipeline` (optional): A string value representing what workflow you want your translations to go through. [Contact sales](mailto:sales@langapi.co) for information on how to customize translation workflows.

# Rest API

## GET /translations

```markdown
# cURL

curl -X GET \
  "https://lang-backend.herokuapp.com/api/v1/translations" \
  -H 'authorization: <YOUR API_KEY>' \
```

> The above request returns a response like this:

```json
{
  "status": "200",
  "message": "OK",  
  "translations": [
      {
          "original_text": "My name is Abhi!",
          "translation": "Me llamo Abhi!",
          "description": "welcome message on landing page",
          "original_language": "en",
          "target_language": "es",
          "is_test": true,
          "status": "pending",
          "parameters": [],
      },
      {
          "original_text": "I have {0} apples",
          "translation": "Tengo {0} manzanas",
          "description": null,
          "original_language": "en",
          "target_language": "es",
          "is_test": true,
          "status": "approved",
          "parameters": [
            {
              "index": 0,
              "type": "argument",
              "plural": null
            }
          ],
      },
  ]
}
```

All translations can be fetched through this endpoint. Using the test API key will return all the machine translations and the prod API key will return all the human translations.

Headers: 

- `authorization`: API key

Response:

- `status`: status code 
- `message`: status message
- `translations`: All the 'production' or 'development' translations depending on the API key.
  - `original_text`: string. A string in original language containing text to be translated.
  - `translation`: string. A string containing the project name you want to request and receive translations for. If you only own one project, this is optional. Otherwise, you must supply a project name.
  - `description`: string. A human-readable string description of the content you are translating. This will be sent to the translator for context. If description is supplied, the phrase and description combination will also be used as a unique identifier for future lookups.
  - `original_language`: string. Language code of target language.
  - `target_language`: string. Language code of target language.
  - `is_test`: boolean. Indicates whether the translation was done by machines or humans.
  - `status`: string. Possible values include "queued", "pending", "available", "approved"
  - `parameters`: If the original text contained variables then each parameter's type is documented
      - `index`: integer. placeholder of parameter in the original string.
      - `type`: string. Possible values include "argument", "select", or "plural".
      - `plural`: string or null. If it's a plural parameter then it denotes a plural bucket, otherwise it's null.

## POST /translations

```markdown
# cURL

curl -X POST \
  "https://lang-backend.herokuapp.com/api/v1/translations" \
  -H 'authorization: <YOUR API_KEY>' \
  -H 'content-type: application/json' \
  -d '{
  "requests": [
    {
      "original_text": "Welcome to Lang",
      "original_language": "en",
      "description": "header text on landing page",
      "languages": ["es"]
    }
  ]
}'
```

> The above request returns a response like this:

```json
{
    "status": "200",
    "message": "OK",
    "job_id": "cjzufipb2009h0708wtcp1rw1"
}
```

Headers: 

- `authorization`: API key

Response: 

- `status`: status code 
- `message`: status message
- `job_id`: string or null. If at least one translation is new, the job ID for the created job is returned. Otherwise, the job ID is null. The job ID corresponds to the ID in the jobs dashboard.


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
| bn    | Bengali                 |
| gu    | Gujarati                |
| kn    | Kannada                 |
| ml    | Malayalam               |
| mr    | Marathi                 |
| pa    | Punjabi                 |
| ta    | Tamil                   |
| te    | Telugu                  |
| ur    | Urdu                    |

If you want support for a language we don't have yet, reach out to us at support@langapi.co. We're always on call and happy to help!

# Changelog

```

```
