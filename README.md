# EBay Account Management PHP SDK

PHP SDK for eBay Account Management APIs, combining REST and GraphQL clients.

## Covered APIs

- **Account V1** — fulfillment policies, return policies, payment policies, seller privileges
- **Account V2** — user preferences, payout settings
- **Finances** — transactions, payouts, seller funds summary
- **GraphQL** — bidding activity and account-related queries

## Specs

OpenAPI specs and the GraphQL schema are in `specs/`.

## REST contract tests

Changes to SDK code, OpenAPI specs, Composer dependencies, or the contract workflow run the three REST specs on pull requests and pushes to `main`; the check can also be started manually. The shared offline runner and PHP adapter discover the SDK facade and configuration from Composer sources, then rewrite its default base URLs to the loopback mock. No API credentials or network calls to eBay are needed.

To reproduce the CI check locally after `composer install`, install the Node dependencies in the shared runner and run:

```sh
node /path/to/account-management-java-sdk/tools/contract-test/lib/runner.cjs \
	--spec-directory specs/openapi -- \
	php /path/to/account-management-java-sdk/tools/contract-test/adapters/php/adapter.php
```

The default suite checks successful responses. Adding `--errors` before `--spec-directory` also tests declared 4xx responses; these currently fail because the SDK surfaces raw Guzzle exceptions instead of decoded Kiota errors.

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.
