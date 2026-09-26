---
title: Reading Locales
comments: true
tags:
    - UI
    - Strings
---

## Reading a locale without variables

=== "`JavaScript`"

    ``` js linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message = await t("helloMessage");

        console.log(message);
    }
    ```

    1. Update path accordingly

=== "`TypeScript`"

    ``` ts linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message: string = await t("helloMessage");

        console.log(message);
    }
    ```

    1. Update path accordingly

??? tip
    Trying to read a locale that doesn't exist neither in the current selected translation nor in the fallback (english) one will return the target key (ex. `"helloMessage"`).

## Reading a locale with variables

If a locale is defined as:

``` json
{
    "helloMessage": "Hello, {{name}}!"
}
```

Then, you need to give it a value for `name`:

=== "`JavaScript`"

    ``` js linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message = await t("helloMessage", { name: 'John Doe' });

        console.log(message);
    }
    ```

    1. Update path accordingly

=== "`TypeScript`"

    ``` ts linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message: string = await t("helloMessage", { name: 'John Doe' });

        console.log(message);
    }
    ```

    1. Update path accordingly

## Reading nested locales

If a locale is defined as:

``` json
{
    "messages": {
        "helloMessage": "Hello, world!"
    }
}
```

Then, you need to type out the entire key, with `.` as the separator:

=== "`JavaScript`"

    ``` js linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message = await t("messages.helloMessage");

        console.log(message);
    }
    ```

    1. Update path accordingly

=== "`TypeScript`"

    ``` ts linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message: string = await t("messages.helloMessage");

        console.log(message);
    }
    ```

    1. Update path accordingly

Alternatively, you can also read the entire `"messages"` key, though doing so is not preferred:

=== "`JavaScript`"

    ``` js linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message = await t("messages");

        console.log(message.helloMessage);
    }
    ```

    1. Update path accordingly

=== "`TypeScript`"

    ``` ts linenums="1"
    import { t } from "../core/locale/i18n.js";  // (1)!

    async function main() {
        const message: Record<string, any> = await t("messages");

        console.log(message.helloMessage);
    }
    ```

    1. Update path accordingly
