---
title: Adding a Locale
comments: true
---

## Adding a new Locale File

To add a locale, first create the locale file under `public/Assets/locales/<language_code>.json`. Make sure it follows the overall structure of the English locale file.

??? tip
    If a locale isn't found in your translation, i18next will automatically fallback to the English locale.

Once you've added the locale file, you'll want to modify the `rovalraLanguage` setting in `core/settings/settingConfig.js` to add your language as an option, in `options: [...]`. Add your language as:

```js
{ label: '<Language> (<Language name in said language>)', value: '<language code>' },
```

Example:

```js
{ label: 'Romanian (Română)', value: 'ro' },
```

### Adding yourself as a Translator

To actually get the **translator badge** and show up in the contributor list:

1. First, add yourself to `src/content/core/configs/userIds.js` to `TRANSLATOR_USER_IDS`. This will give you a translator badge
2. Create a locale under `settings.credits.otherContributions.locales` with a short description stating that you made a locale for that specific language. You will need this in the next step.
3. Add yourself to `src/content/core/configs/otherContributions.ts` to `OTHER_CONTRIBUTIONS.Locales.contributors` as `new Contribution(<roblox user ID>, "locales.<rest of locale key>", "<Pull Request link (optional)>")`. Take the other entries as examples if you need to.

## Adding a locale key

To add a locale key, simply edit the JSON data of the English locale file (`public/Assets/locales/en.json`) to add a new key (ex. `helloWorld`) with a value.

[View how to read a locale](reading-locale.md){ .md-button .md-button--primary }
[View more information about i18next](https://www.i18next.com/){ .md-button }

## Adding a single translation

Submit a translation directly to RoValra.

<div id="translation-tool">

  <div class="translation-field">
    <label for="language">
      <strong>Language</strong>
    </label>

    <select id="language">
      <option value="ro">Romanian (ro)</option>
    </select>
  </div>

  <div class="translation-field">
    <label for="translation-key">
      <strong>Translation key</strong>
    </label>

    <select id="translation-key">
      <option value="">Loading translation keys...</option>
    </select>
  </div>

  <div class="translation-field">
    <label for="english-text">
      <strong>English text</strong>
    </label>

    <div
      id="english-text"
      class="english-preview"
    >
      Select a translation key.
    </div>
  </div>

  <div class="translation-field">
    <label for="translation">
      <strong>Your translation</strong>
    </label>

    <textarea
      id="translation"
      rows="5"
      placeholder="Enter the translated text..."
    ></textarea>
  </div>

  <button
    id="submit-button"
    type="button"
  >
    Submit Translation
  </button>

  <div
    id="translation-status"
    class="translation-status"
    hidden
  ></div>

</div>

<script>
  const SOURCE_URL =
    "https://raw.githubusercontent.com/NotValra/RoValra/refs/heads/main/public/Assets/locales/en.json";

  const API_URL =
    "https://translation-bot.bogdanelsandu2011.workers.dev/translation";

  const languageSelect =
    document.getElementById("language");

  const keySelect =
    document.getElementById("translation-key");

  const englishValue =
    document.getElementById("english-text");

  const translationInput =
    document.getElementById("translation");

  const submitButton =
    document.getElementById("submit-button");

  const status =
    document.getElementById("translation-status");


  function flattenTranslations(
    object,
    prefix = "",
    result = {},
  ) {
    for (const [key, value] of Object.entries(object)) {
      const fullKey =
        prefix
          ? `${prefix}.${key}`
          : key;

      if (typeof value === "string") {
        result[fullKey] = value;
        continue;
      }

      if (
        value !== null &&
        typeof value === "object" &&
        !Array.isArray(value)
      ) {
        flattenTranslations(
          value,
          fullKey,
          result,
        );
      }
    }

    return result;
  }


  function showStatus(
    message,
    type = "success",
  ) {
    status.textContent = message;
    status.hidden = false;

    status.className =
      `translation-status translation-status-${type}`;
  }


  async function loadTranslations() {
    try {
      showStatus(
        "Loading translation keys...",
        "loading",
      );

      const response =
        await fetch(SOURCE_URL);

      if (!response.ok) {
        throw new Error(
          `Failed to load English translations: HTTP ${response.status}`,
        );
      }

      const english =
        await response.json();

      const translations =
        flattenTranslations(english);

      keySelect.innerHTML =
        '<option value="">Select a translation key...</option>';

      for (const [key, value] of Object.entries(translations)) {
        const option =
          document.createElement("option");

        option.value = key;
        option.textContent = key;

        keySelect.appendChild(option);
      }

      window.translationData =
        translations;

      showStatus(
        "Translation keys loaded.",
        "success",
      );

    } catch (error) {
      console.error(error);

      showStatus(
        "Could not load the English translations. Please refresh the page and try again.",
        "error",
      );
    }
  }


  keySelect.addEventListener(
    "change",
    () => {
      const key =
        keySelect.value;

      if (!key) {
        englishValue.textContent =
          "Select a translation key.";

        return;
      }

      const value =
        window.translationData?.[key];

      englishValue.textContent =
        value ?? "English translation not found.";
    },
  );


  async function submitTranslation() {
    /*
     * Remove focus from the translation input
     * before reading its value.
     */
    translationInput.blur();

    const langCode =
      languageSelect.value;

    const key =
      keySelect.value;

    const translation =
      translationInput.value.trim();


    // Empty translation
    if (!translation) {
      showStatus(
        "Please enter a translation before submitting.",
        "error",
      );

      translationInput.focus();

      return;
    }


    // No key selected
    if (!key) {
      showStatus(
        "Please select a translation key.",
        "error",
      );

      return;
    }


    submitButton.disabled = true;

    showStatus(
      "Creating pull request...",
      "loading",
    );


    try {
      const response =
        await fetch(API_URL, {
          method: "POST",

          headers: {
            "Content-Type": "application/json",
          },

          body: JSON.stringify({
            langCode,
            key,
            translation,
          }),
        });


      let data = null;

      try {
        data =
          await response.json();
      } catch {
        // Response wasn't valid JSON.
      }


      // Handle 4xx / 5xx responses
      if (!response.ok) {
        const message =
          data?.error ||
          `Request failed with HTTP ${response.status}.`;

        showStatus(
          message,
          "error",
        );

        return;
      }


      // Handle success=false
      if (!data?.success) {
        showStatus(
          data?.error ||
          "The translation could not be submitted.",
          "error",
        );

        return;
      }


      const pullRequestUrl =
        data.pullRequest?.url;


      if (!pullRequestUrl) {
        showStatus(
          "The translation was submitted, but no pull request URL was returned.",
          "error",
        );

        return;
      }


      showStatus(
        "Translation submitted successfully! Opening the pull request...",
        "success",
      );


      window.open(
        pullRequestUrl,
        "_blank",
        "noopener,noreferrer",
      );


      translationInput.value = "";


    } catch (error) {
      console.error(error);

      showStatus(
        "Could not connect to the translation API. Please try again.",
        "error",
      );

    } finally {
      submitButton.disabled = false;
    }
  }


  submitButton.addEventListener(
    "click",
    submitTranslation,
  );


  loadTranslations();
</script>

<style>
  /*
   * Translation tool
   * Designed to match Zensical / Material styling.
   */

  #translation-tool {
    max-width: 800px;
    margin: 1.5rem 0;
  }


  /*
   * Fields
   */

  .translation-field {
    margin-bottom: 1.5rem;
  }

  .translation-field label {
    display: block;
    margin-bottom: 0.5rem;
    color: var(--md-default-fg-color);
    font-weight: 600;
  }


  /*
   * Selects and textarea
   */

  .translation-field select,
  .translation-field textarea {
    display: block;
    width: 100%;
    box-sizing: border-box;

    padding: 0.7rem 0.8rem;

    font: inherit;
    color: var(--md-default-fg-color);

    background-color: var(--md-default-bg-color);

    border: 1px solid
      var(--md-default-fg-color--lightest);

    border-radius: 0.2rem;

    transition:
      border-color 0.15s ease,
      box-shadow 0.15s ease;
  }


  .translation-field select {
    cursor: pointer;
  }


  .translation-field textarea {
    min-height: 120px;
    resize: vertical;
  }


  /*
   * Focus state
   */

  .translation-field select:focus,
  .translation-field textarea:focus {
    outline: none;

    border-color:
      var(--md-accent-fg-color);

    box-shadow:
      0 0 0 1px
      var(--md-accent-fg-color);
  }


  /*
   * English preview
   */

  .english-preview {
    padding: 0.9rem 1rem;

    color: var(--md-default-fg-color);

    background-color:
      var(--md-code-bg-color);

    border:
      1px solid
      var(--md-default-fg-color--lightest);

    border-radius: 0.2rem;

    white-space: pre-wrap;
    overflow-wrap: anywhere;
  }


  /*
   * Submit button
   *
   * Uses Zensical's existing button classes.
   */

  #submit-button {
    display: inline-block;

    margin-top: 0.25rem;

    padding:
      0.625rem
      1rem;

    font: inherit;
    font-weight: 500;

    color:
      var(--md-primary-bg-color);

    background-color:
      var(--md-primary-fg-color);

    border:
      1px solid
      var(--md-primary-fg-color);

    border-radius: 0.2rem;

    cursor: pointer;

    transition:
      background-color 0.15s ease,
      border-color 0.15s ease,
      opacity 0.15s ease,
      box-shadow 0.15s ease;
  }


  #submit-button:hover {
    background-color:
      var(--md-primary-fg-color--dark);

    border-color:
      var(--md-primary-fg-color--dark);
  }


  #submit-button:focus-visible {
    outline: 2px solid
      var(--md-accent-fg-color);

    outline-offset: 2px;
  }


  #submit-button:disabled {
    opacity: 0.6;
    cursor: wait;
  }


  /*
   * Status message
   */

  .translation-status {
    margin-top: 1rem;
    padding: 0.8rem 1rem;

    border-radius: 0.2rem;

    border: 1px solid
      var(--md-default-fg-color--lightest);

    color:
      var(--md-default-fg-color);

    background:
      var(--md-code-bg-color);

    white-space: pre-wrap;
  }


  /*
   * Success
   */

  .translation-status-success {
    border-color: #4caf50;

    background-color:
      rgba(76, 175, 80, 0.08);
  }


  /*
   * Error
   */

  .translation-status-error {
    border-color: #ef5350;

    background-color:
      rgba(239, 83, 80, 0.08);
  }


  /*
   * Loading
   */

  .translation-status-loading {
    opacity: 0.85;
  }


  /*
   * Dark theme adjustments
   *
   * Zensical uses the "slate" scheme for dark mode.
   */

  [data-md-color-scheme="slate"]
  .translation-status-success {
    background-color:
      rgba(76, 175, 80, 0.12);
  }


  [data-md-color-scheme="slate"]
  .translation-status-error {
    background-color:
      rgba(239, 83, 80, 0.12);
  }


  /*
   * Mobile
   */

  @media screen and (max-width: 600px) {
    #translation-tool {
      width: 100%;
    }

    #submit-button {
      width: 100%;
    }
  }
</style>

## More Info

The locales use `i18next` under the hood. For more information, visit <https://www.i18next.com/>.
