# JSON Translation Script

This Python script automates translating a base JSON language file (en_us.json) into multiple target languages using the Google Translate API via the deep_translator library. It also supports reusing existing translations to speed up the process.

## Features

- Loads and validates the base JSON file.
- Translates all string values recursively (including nested dictionaries and arrays).
- Skips URLs (values starting with "http").
- Optionally reuses existing translations if available.
- Periodically reports translation progress.
- Outputs neatly formatted JSON files for each language.

## Prerequisites

- Python 3.7 or higher
- Install the required package:
```
  pip install deep-translator
```

## How It Works

1. Load Source JSON
   The script loads src/assets/lang/en_us.json and validates that it is proper JSON.

2. Target Languages
   It attempts translation for each language code listed in the target_languages array.

3. Handling Existing Translations
   If the -skip flag is passed when running the script, it tries to load existing translations and reuse any non-empty existing translations to avoid overwriting.

4. Translation Process
   For each string:
   - If it is a URL (starts with "http"), it skips translation.
   - Otherwise, it uses GoogleTranslator to translate the string into the target language.
   - It updates the JSON structure in-place.

5. Progress Display
   Every 3 seconds during translation, it prints how many lines have been completed.

6. Save Results
   After translating, it saves the new JSON file in src/assets/lang/ under the format {language_code}.json, formatted with indentation for easy readability.

## Usage

Translate everything (overwrite if any existing translations exist):
```
python translate.py
```

Translate while reusing existing translations (skip already translated entries):
```
python translate.py -skip
```

## File Structure

- src/assets/lang/en_us.json — Source file
- src/assets/lang/{language_code}.json — Output files for each target language

## Important Notes

- If a translation fails (for example, due to API rate limits or network errors), the script prints the error and continues.
- The script assumes en_us.json is properly formatted and all strings intended for translation are in it.
- Make sure your IP or environment is allowed to use Google Translate API through deep_translator, or else you may encounter rate-limiting issues.
