These settings are for users who want to further customize the behavior or appearance of uMatrix.

Keep in mind that any of these raw settings may be removed in the future, more may be added, or existing ones may become mainstream settings with a dedicated UI. Some of these raw settings may exist for experimental purpose only.

To restore any one setting to its original built-in value, just remove the whole setting.

***
#### `disableCSPReportInjection`

- Type: boolean
- `false` (default): do inject a `Content-Security-Policy-Report-Only` header in response headers, as needed.
- `true`: never inject a `Content-Security-Policy-Report-Only` header in response headers.
    - Disabling the injection of `Content-Security-Policy-Report-Only` will render uMatrix unable to report to you whether web workers are used by a web page when these are not to be blocked.

The `Content-Security-Policy-Report-Only` is currently injected by uMatrix to detect the use of web workers on a site, when web workers are not forbidden.

***

#### `framePlaceholder`

- Type: boolean
- `true` (default): replace non-collapsed blocked frame with a placeholder.
- `false`: do not replace non-collapsed blocked frame with a placeholder.

***

#### `framePlaceholderBackground`

- Type: string
- `default` (default): use the background value from `placeholderBackground`.
- Otherwise a valid CSS `background` property value to be used as is.

***

#### `framePlaceholderDocument`

- Type: string
- An HTML document source with no newline character.

***

#### `imagePlaceholder`

- Type: boolean
- `true` (default): replace non-collapsed blocked image with a placeholder.
- `false`: do not replace non-collapsed blocked image with a placeholder.

Use `false` to prevent the use of placeholder for blocked images and thus eliminate the ability of image placeholder styling information to be used as fingerprint information.

***

#### `imagePlaceholderBackground`

- Type: string
- `default` (default): use the background value from `placeholderBackground`.
- Otherwise a valid CSS `background` property value to be used as is.

Note that using a custom value for image placeholder can make you fingerprintable.

***

#### `imagePlaceholderBorder`

- Type: string
- `default` (default): : use the border value from `placeholderBorder`.
- Otherwise a valid CSS `border` property value to be used as is.

Note that using a custom value for image placeholder can make you fingerprintable.

***

#### `placeholderBackground`

- Type: string
- Default value is an internal CSS background value.
- Otherwise a valid CSS background property to be used as placeholder background.

Override this value if you want to customize the background value for all placeholders.

Note that using a custom value for image placeholder can make you fingerprintable.

***

#### `placeholderBorder`

- Type: string
- Default value is an internal CSS border value.
- Otherwise a valid CSS border property to be used as placeholder background.

Override this value if you want to customize the border value for all placeholders.

Note that using a custom value for image placeholder can make you fingerprintable.
