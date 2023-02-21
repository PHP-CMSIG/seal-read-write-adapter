<div align="center">
    <img alt="Schranz Search Logo with a Seal on it with a magnifying glass" src="https://avatars.githubusercontent.com/u/120221538?s=400&v=5" width="200" height="200">
</div>

<h1 align="center">Schranz Search SEAL <br /> Read Write Adapter</h1>

<br />
<br />

The `ReadWriteAdapter` allows to use one adapter instance for reading
and one for writing. This is useful if you want to reindex something
without a downtime.

> **Note**:
> This is part of the `schranz-search/schranz-search` project create issues in the [main repository](https://github.com/schranz-search/schranz-search).

> **Warning**:
> This project is heavily under development and not ready for production.

## Installation

Use [composer](https://getcomposer.org/) for install the package:

```bash
composer require schranz-search/seal schranz-search/seal-read-write-adapter
```

## Usage

To use the adapter an instance of `ReadWriteAdapter` need to be created
which get a `$readAdapter` and `$writeAdapter` which are instances of the
`AdapterInterface`.

The following code shows how to create an Engine using this Adapter:

```php
<?php

use Schranz\Search\SEAL\Adapter\Elasticsearch\ElasticsearchAdapter;
use Schranz\Search\SEAL\Adapter\ReadWrite\ReadWriteAdapter;
use Schranz\Search\SEAL\Engine;

$readAdapter = new ElasticsearchAdapter(/* .. */); // can be any adapter
$writeAdapter = new ElasticsearchAdapter(/* .. */); // can be any adapter

$engine = new Engine(
    new ReadWriteAdapter(
        $readAdapter,
        $writeAdapter
    ),
    $schema,
);
```

Via DSN for your favorite framework:

```env
multi://readAdapter?adapters[]=writeAdapter
read-write://readAdapter?write=multiAdapter
```

> **Note**
> Read a document and partial update it based on the read document should be avoided
> when using this adapter, as the read document could already be outdated. So always
> fully update the document and never do based on read documents.
> Have a look at the `MultiAdapter` to write into read and write adapter.

## Authors

- [Alexander Schranz](https://github.com/alexander-schranz/)
- [The Community Contributors](https://github.com/schranz-search/schranz-search/graphs/contributors)
