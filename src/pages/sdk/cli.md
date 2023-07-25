---
title: CLI
description: Learn how to use the CLI.
---

{% callout type="note" title="CLI under development" %}
Because we're so early, the only CLI command currently available is `docs`. We're working hard to add more commands, so stay tuned!
{% /callout %}

`polyfact` uses the following command structure for documentation generation:

```bash
npx polyfact docs <folder> [options]
```

## Arguments

- `<folder>`: This is the path of the folder from which to generate the documentation. This argument is mandatory.

## Options

- `-n, --name <doc_name>`: This is the name of the documentation. If not provided, it defaults to 'id'.

- `-d, --deploy <subdomain>`: This option allows you to provide a subdomain to which the generated documentation will be deployed.

- `--doc_id <doc_id>`: If the doc_id has already been generated, you can send it as an argument here.

## Examples

```bash
# Generate documentation from the src folder with the default parameters
npx polyfact docs ./src

# Generate documentation with a specific name from the src folder and output to a specific folder
npx polyfact docs ./src --name "my-documentation"

# Generate documentation and deploy it to a specific subdomain
npx polyfact docs ./src --deploy my-subdomain
```
