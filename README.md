<div align="center">
<a href="https://github.com/playwright-php"><img src="https://github.com/playwright-php/.github/raw/main/profile/playwright-php.png" alt="Playwright PHP" /></a>

&nbsp; ![CI](https://img.shields.io/github/actions/workflow/status/playwright-php/setup-playwright/test.yaml?branch=main&label=Tests&color=1D8D23&labelColor=09161E&logoColor=FFFFFF)
&nbsp; ![Release](https://img.shields.io/github/v/release/playwright-php/setup-playwright?label=Stable&labelColor=09161E&color=1D8D23&logoColor=FFFFFF)
&nbsp; ![License](https://img.shields.io/github/license/playwright-php/setup-playwright?label=License&labelColor=09161E&color=1D8D23&logoColor=FFFFFF)

</div>

# Setup Playwright (for PHP)

Sets up the runner for [Playwright for PHP](https://playwright-php.dev):
- install `@playwright` JS library globally
- download the browser binaries (default: Chrome)

## Usage

```yaml
# .github/workflows/test.yml
name: PHP Tests
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: playwright-php/setup-playwright@v1
        with:
          browsers: chrome      # default value
          
      - uses: shivammathur/setup-php@v2
        with:
          php-version: '8.4'
      - run: composer install
      - run: vendor/bin/phpunit
```

## Outputs

The action exposes two outputs:

- `playwright-version`: the installed Playwright CLI version
- `installed-browsers`: a JSON list of the browsers that were installed

## Configuration

| Option               | Default  | Allowed values                                             | Notes                                                                                                                                                                    |
|----------------------|----------|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `browsers`           | `chrome` | `chrome`, `chromium`, `firefox`, `webkit`, `msedge`, `all` | `msedge` only on Windows runners                                                                                                                                         |
| `playwright-version` | `latest` | Any valid npm specifier (for the `playwright` package)     | Leave `latest` to track upstream.                                                                                                                                        |
| `with-deps`          | `auto`   | `true`, `false`, `auto`                                    | `auto` appends Playwright's `--with-deps` flag on Linux runners.                                                                                                         |
| `browsers-path`      |          | Directory path                                             | Exports `PLAYWRIGHT_BROWSERS_PATH` so downloads land in your cache. Leave blank for Playwright defaults (`~/.cache/ms-playwright`, `%LOCALAPPDATA%\ms-playwright`, etc.) |

## License

This package is released by the [Playwright PHP](https://playwright-php.dev)
project under the MIT License. See the [LICENSE](LICENSE) file for details.
