# action-monorepo-package-release

_action-monorepo-package-release_ is a workflow for [GitHub Actions] used by the [fundamend.dev] ecosystem.
It releases individual monorepo packages after they have been split from the main repository into their own repositories with [action-splitsh-lite].

It will:

- Check if the version in `package.json` has changed
- If so, tag the latest commit with the new version number
- Create a new Github release with the content of the changelog
- Publish to NPM (if activated)

## Usage

In your package, create a workflow that uses _action-monorepo-package-release_, like so:

```yaml
name: Release

on: [push]

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - name: Release
        uses: fundamend/action-monorepo-package-release@main
        with:
          publish-npm-package: true
          github-token: ${{ secrets.GITHUB_TOKEN }}
          npm-token: ${{ secrets.NPM_TOKEN }}
```

The action takes the following inputs:

| Key                   | Description                                                        |
| --------------------- | ------------------------------------------------------------------ |
| `publish-npm-package` | Wether or not an NPM package should be published (default `false`) |
| `github-token` \*     | Automatically filled by Github                                     |
| `npm-token`           | required if `publish-npm-package` is set to `true`                 |

The \* indicates mandatory input.

The `npm-token` secret is filled if an `NPM_TOKEN` secret is set in your actions secrets.

## License

[MIT]

[action-splitsh-lite]: https://github.com/fundamend/action-splitsh-lite
[fundamend.dev]: https://fundamend.dev
[github actions]: https://docs.github.com/en/actions
[github]: https://github.com/
[mit]: https://choosealicense.com/licenses/mit/
