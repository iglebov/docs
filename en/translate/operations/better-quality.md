---
title: How to improve translation accuracy in {{ translate-full-name }}
description: In this article, you will learn how to improve translation accuracy.
---

# How to improve the accuracy of translations

To increase the accuracy of translations:

* [Specify the source language](#with-source-language). Some words are written the same in different languages, but have different meanings. If the model detects the wrong source language, these words are translated differently.
* [Specify your translation glossary](#with-glossary). A word can be translated different ways. For example, the English word _oil_ can be translated into Russian as _масло_ or _нефть_. You can use a glossary to indicate the proper translation of a word or phrase. You can learn more about glossaries [here](../concepts/glossary.md).

## Getting started {#before-you-begin}

{% include [curl](../../_includes/curl.md) %}

{% include [bash-windows-note](../../_includes/translate/bash-windows-note.md) %}

{% include [ai-before-beginning](../../_includes/translate/ai-before-beginning.md) %}


## Specify the source language {#with-source-language}

Words are sometimes written the same in different languages but translated differently. For example, the word <q>angel</q> means a spiritual being in English, while in German it means a fishing rod. If the text you provide contains such words, {{ translate-short-name }} may detect the wrong source language.

To avoid mistakes, specify the source language in the `sourceLanguageCode` field:

{% list tabs group=programming_language %}

- Bash {#bash}

    ```json
    {
        "folderId": "<folder_ID>",
        "texts": ["angel"],
        "targetLanguageCode": "ru",
        "sourceLanguageCode": "de"
    }
    ```

    Where:

    * `folderId`: Folder ID received [before starting](#before-begin).
    * `texts`: Text to translate as a list of strings.
    * `targetLanguageCode`: Target [language](../concepts/supported-languages.md). You can get the language code together with a [list of supported languages](list.md).
    * `sourceLanguageCode`: Source language.

    Save the request body to a file (for example, `body.json`) and submit the file using the [translate](../api-ref/Translation/translate) method:

    {% include [translate-file](../../_includes/translate/translate-file.md) %}

    Where `IAM_TOKEN` is the IAM token received [before starting](#before-begin).

    This returns a translation from the correct language:

    {% include [with-source-language](../../_untranslatable/translate/with-source-language.md) %}

{% endlist %}

## Specify your translation glossary {#with-glossary}

A word can be translated different ways. For example, the English word _oil_ can be translated into Russian as _масло_ or _нефть_. To improve the accuracy of translations, use a [glossary](../concepts/glossary.md) of your terms and phrases with a single translation.

Specify the glossary in the `glossaryConfig` field. Currently, you can only pass a glossary as an array of text pairs.

In the `sourceLanguageCode` field, specify the source language. This field is required when you use glossaries:

{% list tabs group=programming_language %}

- Bash {#bash}

    {% include [with-glossary-req](../../_untranslatable/translate/with-glossary-req.md) %}

    Where:

    * `sourceLanguageCode`: Source [language](../concepts/supported-languages.md). You can get the language code together with a [list of supported languages](list.md).
    * `targetLanguageCode`: Target language.
    * `texts`: Text to translate as a list of strings.
    * `folderId`: Folder ID received [before starting](#before-begin).

    Save the request body to a file (for example, `body.json`) and submit the file using the [translate](../api-ref/Translation/translate) method:

    {% include [translate-file](../../_includes/translate/translate-file.md) %}

    Where `IAM_TOKEN` is the IAM token received [before starting](#before-begin).

    The response will contain a translation based on the terms from your glossary:

    {% include [with-glossary-ans1](../../_untranslatable/translate/with-glossary-ans1.md) %}

    Without the glossary, the translation would be:

    {% include [with-glossary-ans2](../../_untranslatable/translate/with-glossary-ans2.md) %}

{% endlist %}

## Escaping text {#screen}

To skip translation of certain text fragments, specify the `HTML` text format in the request body and escape the fragments that do not require translation using the `<span>` tag with the `translate=no` attribute. For example:

{% list tabs group=programming_language %}

- Bash {#bash}

   ```json
   {
       "format": "HTML",
       "texts": [
           "The e-mail has been changed. The new password is **<span translate=no>**%\$Qvd14aa2NMc**</span>**"
       ]
   }
   ```

   Where:

   * `format`: Text format.
   * `texts`: Text to translate as a list of strings.

   The response will contain untranslated text inside the `<span>` tag:

   ```json
   {
       "translations": [
           {
               "text": "L'e-mail a été modifié. Le nouveau mot de passe est **<span translate="no">**%\$Qvd14aa2NMc**</span>**"
           }
       ]
   }
   ```

{% endlist %}

## Checking words for typos {#with-speller}

Misspelled words may be translated incorrectly or transliterated. For example, the word <q>hellas</q> is translated as <q>эллада</q>. If the same word is misspelled, let's say as <q>helas</q>, it will be translated as <q>хелас</q>. To check spelling, use the `speller` parameter:

{% list tabs group=programming_language %}

- Bash {#bash}

    ```json
    {
      "sourceLanguageCode": "en"
      "targetLanguageCode": "ru",
      "texts": [
        "helas"
        ],
      "folderId": "<folder_ID>",
      "speller": true
    }
    ```

    Where:

    * `sourceLanguageCode`: Source [language](../concepts/supported-languages.md). You can get the language code with a [list of supported languages](list.md).
    * `targetLanguageCode`: Target language.
    * `texts`: Text to translate as a list of strings.
    * `folderId`: Folder ID received [before starting](#before-begin).
    * `speller`: Parameter that enables a spelling check.

    Save the request body to a file (for example, `body.json`) and submit the file using the [translate](../api-ref/Translation/translate) method:

    {% include [translate-file](../../_includes/translate/translate-file.md) %}

    Where `IAM_TOKEN` is the IAM token received [before starting](#before-begin).

    The response will contain a translation of the word checked for spelling:

    {% include [with-speller-ans1](../../_untranslatable/translate/with-speller-ans1.md) %}

    If no spelling check is enabled (`"speller": false`), the word will be translated as follows:

    {% include [with-speller-ans2](../../_untranslatable/translate/with-speller-ans2.md) %}

{% endlist %}
