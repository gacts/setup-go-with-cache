<p align="center">
  <img src="https://user-images.githubusercontent.com/7326800/201531733-1bf653f6-c303-435f-8ec3-2e5f7d45f4c6.png" alt="Logo" width="100" />
</p>

# Setup Go environment with a Cache

![Release version][badge_release_version]
[![Build Status][badge_build]][link_build]
[![License][badge_license]][link_license]

Composite GitHub Action which combines the perfect pairing of [actions/setup-go](https://github.com/actions/setup-go) with [actions/cache](https://github.com/actions/cache) for
the caching of both the Golang module and build caches _(the original action idea was taken
[here](https://github.com/magnetikonline/action-golang-cache))_.

Reducing all these workflow steps:

```yaml
steps:
  - name: Setup Golang
    uses: actions/setup-go@v3
    with:
      go-version: 1.22

  - name: Setup Golang caches
    uses: actions/cache@v3
    with:
      path: |
        ~/.cache/go-build
        ~/go/pkg/mod
      key: ${{ runner.os }}-golang-${{ hashFiles('**/go.sum') }}
      restore-keys: |
        ${{ runner.os }}-golang-
```

Down to this:

```yaml
steps:
  - {uses: gacts/setup-go-with-cache@v1, with: {go-version: 1.22}}
```

Or using `go-version-file` for version selection:

```yaml
steps:
  - {uses: gacts/setup-go-with-cache@v1, with: {go-version-file: go.mod}}
```

> [!TIP]
> Use [Dependabot][use_dependabot] to maintain your `gacts/setup-go-with-cache` version updated in your GitHub workflows.

## Support

[![Issues][badge_issues]][link_issues]
[![Issues][badge_pulls]][link_pulls]

If you find any action errors - please, [make an issue][link_create_issue] in the current repository.

## License

This is open-sourced software licensed under the [MIT License][link_license].

[badge_build]:https://img.shields.io/github/actions/workflow/status/gacts/setup-go-with-cache/test.yml?branch=master&maxAge=30
[badge_release_version]:https://img.shields.io/github/release/gacts/setup-go-with-cache.svg?maxAge=30
[badge_license]:https://img.shields.io/github/license/gacts/setup-go-with-cache.svg?longCache=true
[badge_issues]:https://img.shields.io/github/issues/gacts/setup-go-with-cache.svg?maxAge=45
[badge_pulls]:https://img.shields.io/github/issues-pr/gacts/setup-go-with-cache.svg?maxAge=45

[link_build]:https://github.com/gacts/setup-go-with-cache/actions
[link_license]:https://github.com/gacts/setup-go-with-cache/blob/master/LICENSE
[link_issues]:https://github.com/gacts/setup-go-with-cache/issues
[link_create_issue]:https://github.com/gacts/setup-go-with-cache/issues/new
[link_pulls]:https://github.com/gacts/setup-go-with-cache/pulls

[use_dependabot]:https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/keeping-your-actions-up-to-date-with-dependabot
