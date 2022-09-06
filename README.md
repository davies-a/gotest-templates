## Templates for gotests

Repository holding templates for generating unit tests in golang using `gotests`.

The upstream repo documentation is [here](https://github.com/cweill/gotests), but it's not particularly clear.

## Usage

Point `gotests` at the folder containing your .tmpl files - in the case of this repo, that's `templates/testify_wanterr`.

In VSCode this can be set using the settings file, adding the following to your `settings.json`:
```json
{
    "go.generateTestsFlags":[
        "-template_dir=/path/to/repo/templates/template_name"
    ]
}
```

Alternatively, you can set this OS-wide by setting `GOTESTS_TEMPLATE_DIR=/path/to/repo/templates/template_name`.

## Notes on the upstream package:

The templates in the upstream repo `templates` directory weren't working when I used them. These were caused by an error with the `.Named`
attribute in the template and references to it. However, we tend to use table tests with a name attribute to the struct; as a result there
isn't much value to the Named attribute (this may have caused it to disappear - not sure).

## The testify_wanterr templates:
These largely mirror the regular templates used by `gotests`, with a couple of differences: 
* Sample table tests are spawned to make it easier to fill these out.
* `wantErr` is now an error object that is checked using testify to see whether the error received matches the one expected.
* The creation of the `got` variable (and `err`) within tests is moved to always be outside of the tests; this is deliberate to make debugging easier,
and in order to improve readability.

