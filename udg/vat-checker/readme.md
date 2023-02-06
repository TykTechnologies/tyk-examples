# VAT Checker GQL API

This is an extremely basic example of what Universal Data Graph is capable of.

## Use case

REST API returns data that my app doesn't really need (i.e. detailed registration address of the company registered with the VAT number) and I would rather only fetch the data I need.

I want to wrap an existing REST API with GraphQL, quickly and without writing my own code.

### REST API DataSource

REST API documentation can be found [here](https://www.vatcomply.com/documentation).
Example graph is using:
* GET method
* URL https://api.vatcomply.com/vat?vat_number={vat_number}

Sample response:
```
{
  "valid": true,
  "vat_number": "810462783B01",
  "name": "SHELL CHEMICALS EUROPE B.V.",
  "address": "WEENA 00070 3012CM ROTTERDAM",
  "country_code": "NL"
}
```

## GraphQL API based on REST

REST response has been "translated" into a GraphQL schema. Additionally comments have been added in the schema, so that each field can be documented in the GQL Playground.

If you want to only check if the VAT Code is valid or not use the following query:

```
query {
  vatcheck(code: "PL5832768926") {
    valid
  }
}
```

To request information about the company name registered with that VAT number:

```
query {
  vatcheck(code: "PL5832768926") {
    valid
    name
  }
}
```

