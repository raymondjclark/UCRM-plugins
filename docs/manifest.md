# Plugin manifest
The `manifest.json` file contains all needed information about the plugin and is required by UCRM.

## Example
```json
{
    "version": "1",
    "information": {
        "name": "ubnt__dummy-plugin",
        "displayName": "Dummy Plugin - documentation example",
        "description": "This plugin does nothing at all and is used only as a documentation example.",
        "url": "https://github.com/Ubiquiti-App/UCRM-plugins/docs/manifest.md",
        "version": "1.0.0",
        "ucrmVersionCompliancy": {
            "min": "2.13.0-beta1",
            "max": null
        },
        "author": "Ubiquiti Networks, Inc."
    },
    "configuration": [
        {
            "key": "requiredConfigurationField",
            "label": "Configuration field required by the plugin",
            "description": "Please provide information required by this field.",
            "required": 1
        },
        {
            "key": "optionalConfigurationField",
            "label": "An optional and not important configuration field",
            "required": 0
        },
        {
            "key": "welcomeText",
            "label": "Welcome text",
            "description": "This can be very long text with new lines.",
            "required": 0,
            "type": "textarea"
        },
        {
            "key": "paymentMatchAttribute",
            "label": "Match by attribute",
            "description": "Choose by which attribute will the payments be matched.",
            "required": 1,
            "type": "choice",
            "choices": {
              "Invoice number": "invoiceNumber",
              "Client ID": "clientId",
              "Client User Ident": "clientUserIdent",
              "This is label": "thisIsValue"
            }
        },
        {
            "key": "startDate",
            "label": "Start date",
            "required": 0,
            "type": "date"
        },
        {
            "key": "startDateTime",
            "label": "Start date with time",
            "required": 0,
            "type": "datetime"
        },
        {
            "key": "isBoolean",
            "label": "Check this if you want it to be true.",
            "required": 0,
            "type": "checkbox"
        },
    ]
}
```

## Structure

### version
Determines version of the configuration file, for now only possible value is "1".

### information
Contains information describing the plugin.
- `name` - lowercase name of the plugin (can contain dashes `-` and underscores `_`), plugin folder name is determined by this
- `displayName` - name of the plugin as displayed on UCRM frontend
- `description` - longer description of the plugin (e.g. what it does)
- `url` - link to the plugin page
- `version` - version of the plugin as displayed on UCRM frontend
- `ucrmVersionCompliancy` - defines minimum and maximum version of UCRM this plugin supports, minimum must be always defined, maximum can be `null`
- `author` - author of the plugin as displayed on UCRM frontend

### configuration
Determines configuration keys of the plugin. Frontend configuration form is generated from this and the values are then saved to [`data/config.json`](file-structure.md#dataconfigjson) file.

Contains an array of items. Each item is defined as follows:
- `key` - property key
- `label` - label of the property as displayed in UCRM
- `description` (optional) - description of the property, displayed under the form input in UCRM
- `required` (optional, default: `1`) - whether the property is required or optional, configuration cannot be saved without required properties
- `type` (optional, default: `text`) - type of the configuration item, will render appropriate form input in UCRM
    - available as of UCRM 2.13.0-beta1
    - possible values are:
        - `text` - standard text input
        - `textarea` - multi-line text
        - `checkbox` - true/false values
        - `choice` - dropdown list with pre-defined options (needs `choices` definition, see below)
        - `date` - date input with calendar
        - `datetime` - date and time input with calendar
        - `file` - file upload input (the file will have name based on the `key` definition, the filename will be saved in [`data/config.json`](file-structure.md#dataconfigjson) and the file itself will be saved in [`data/files`](file-structure.md#datafiles-directory) directory)
- `choices` (optional) - defines possible options for `choice` type (see manifest example above)
