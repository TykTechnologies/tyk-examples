# Geo Information about the World GQL API

This is a fairly easy example of what Universal Data Graph can do when given multiple datasources of different origins.

## Use case

I have a GQL API that is returning a lot of infomation about the domain that I am interested in, but not everything. On the other hand, there's this REST API I have access to, that would fit in perfectly with what GQL is giving me already. I need an easy way to use both within the same query request.

In case of this example we have a GQL API returning rich information about countries and continents but it's missing geocoding features - it is impossible to know where certain capitals are exactly located, so if it were to be used for an app that is supposed to display maps for example, it would be difficult.

We will extend this GQL API with geocoding information coming from a REST API.

### GQL API Datasource

We're using a very well-known public GQL API service [Trevorblades](https://countries.trevorblades.com/). This service can be accessed via GraphiQL Playground but also there's extensive documentation that can be found [here](https://github.com/trevorblades/countries).

In the example we're using only `country` and `continent` queries. We've skipped `language` query completely, though `type language` is still included in the response.

### REST API Datasource

This exmaple is using geocode.xyz free service to access information about geo location of capitals returned from GQL API above.

Documentation for the datasource can be found [here](https://geocode.xyz/api).

We will use the following request to get waht we need:

```
curl --location --request GET 'https://geocode.xyz/?locate=<capital name from GQL API>&geoit=JSON
```
And example response:

```
{
    "standard": {
        "addresst": {},
        "statename": {},
        "city": "Gdansk",
        "prov": "PL",
        "countryname": "Poland",
        "postal": {},
        "confidence": "0.90"
    },
    "longt": "18.60327",
    "alt": {
        "loc": [
            {
                "longt": "18.6068505374106",
                "prov": "PL",
                "city": "Gdańsk",
                "postal": "pomorskie",
                "score": "33159",
                "latt": "54.3555773032963"
            },
            {
                "longt": "18.4853247908745",
                "prov": "pomorskie",
                "city": "Gdańsk",
                "postal": "80-298",
                "score": "263",
                "latt": "54.3674100760456"
            },
            {
                "longt": "18.60685",
                "prov": "PL",
                "city": "Gdansk",
                "countryname": "Poland",
                "postal": "pomorskie",
                "region": {},
                "latt": "54.35558"
            }
        ]
    },
    "elevation": {},
    "latt": "54.36279"
}
```

We will use just 2 values from it: `latt` and `longt`.

**Note**

In data graph (UDG) schema we will reflect the field names as `latt` and `longt`, which is not entirely intuitive, but it means UDG engine will do all the response parsing automatically in the background without user having to add additional configurations. It is possible to also rename the fields to `lattitude` and `longitude` which will be showed in another example.

## What was achieved?

Combining both APIs means we now have access to both country information and geocoding for capital in one query and instead of using two separate services, all is returned in one go.

### Try it out!

To check some info about Poland you can send the following query:

```
query {
  country(code: "PL") {
    code
    name
    capital
    capitalCoordinates {
      latt
      longt
    }
  }
}
```

**Note**

geocode.xyz is apublic API that does not require any API key or other auth, but that means there are certain rate limits set when you access it. When running larger queries like for example:
```
query {
  countries {
    name
    capital
    capitalCoordinates {
      latt
      longt
    }
  }
}
```
you might hit those limits and not get a full response. But that's strictly the datasource limitation.


