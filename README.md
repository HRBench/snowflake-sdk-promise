# snowflake-sdk-promise [![npm](https://img.shields.io/npm/v/snowflake-sdk-promise.svg)](https://www.npmjs.com/package/snowflake-sdk-promise) [![node](https://img.shields.io/node/v/snowflake-sdk-promise.svg)](https://www.npmjs.com/package/snowflake-sdk-promise)

A Promise-based interface to your [Snowflake](https://www.snowflake.net/) data warehouse.

This is a wrapper for the [Snowflake SDK](https://www.npmjs.com/package/snowflake-sdk) for Node.js. It provides a Promise-based API instead of the core callback-based API.

## Installation

* `npm i snowflake-sdk-promise`

## Basic usage

```typescript
import { Snowflake } from 'snowflake-sdk-promise';

async function main() {
  const snowflake = new Snowflake({
    account: '<account name>',
    username: '<username>',
    password: '<password>',
    database: 'SNOWFLAKE_SAMPLE_DATA',
    schema: 'TPCH_SF1',
    warehouse: 'DEMO_WH'
  });

  const rows = await snowflake.execute(
    'SELECT COUNT(*) FROM CUSTOMER WHERE C_MKTSEGMENT=:1',
    ['AUTOMOBILE']
  );

  console.log(rows);
}

main();
```

## Connecting

The constructor takes up to three arguments:

`new Snowflake(connectionOptions, [ loggingOptions, [ configureOptions ] ])`
OR
`new SnowflakePool(connectionOptions, [ loggingOptions, [ configureOptions ] ])`

* `connectionOptions`
  * Supported options are here: <https://docs.snowflake.net/manuals/user-guide/nodejs-driver-use.html#required-connection-options>
* `loggingOptions`
  * `logSql` (optional, function): If provided, this function will be called to log SQL
    statements. For example, set `logSql` to `console.log` to log all issued SQL
    statements to the console.
  * `logLevel` (optional: `"ERROR" | "WARN" | "DEBUG" | "INFO" | "TRACE"`): Turns on
    SDK-level logging.
* `configureOptions`
  * `ocspFailOpen` (optional, boolean) (default: `true`): Enables OCSP fail-open
    functionality. See <https://www.snowflake.com/blog/latest-changes-to-how-snowflake-handles-ocsp/> for more information.

## More examples

* [Streaming result rows](examples/streaming.js)
* [Using traditional Promise `then` syntax (and older versions of Node.js)](examples/oldSchool.js)
    * Node v6.9.5 is the oldest supported version
* [Turn on logging](examples/logging.js)
* [Advanced TS Example with Singleton](examples/useLocalInstance.ts)
* [Advanced TS Example with Singleton using a Snowflake Connection Pool](examples/useLocalInstance.ts)

## Credits

This project has started as a fork of [snowflake-promise](https://github.com/natesilva/snowflake-promise)
