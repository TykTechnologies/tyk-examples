# React Conferences in Europe GQL API

This examples shows how two different GQL APIs can be stitched together and become a Tyk Universal Data Graph.

## Use case

I have a GQL API that is returning a lot of infomation about the domain that I am interested in, but not everything. But, there's this other GQL API I have access to, that would fit in perfectly with what GQL is giving me already. I need an easy way to use both within the same query request.

In this example we have a great GQL API that returns information about React Conferences in Europe, but due to the nature of a frontend app we're building it would be good to have a country flag returned as part of the response, which needs to be taken from elsewhere.

### GQL API DataSources

We will use [React Finland](https://api.react-finland.fi/graphql) public GQL API to obtain all the information about React Conferences. 

We're also using a very well-known public GQL API service [Trevorblades](https://countries.trevorblades.com/). This service can be accessed via GraphiQL Playground but also there's extensive documentation that can be found [here](https://github.com/trevorblades/countries).
From this one, only `emoji` will be used and in the data graph it will be renamed to `flag`.

## What was achieved?

Combining both APIs means we now have access to full conference details that the React Finland stores, but also we've extended their API with a country flag information. A frontend engineer will now only have to make a single API call to get all the information needed to build the app UI.

### Try it out!

Let's get some conference names, their dates, locations and who organized them:

```graphql
query {
  conferences {
    name
    year
    locations {
      name
      country {
        code
        name
        flag
      }
    }
    organizers {
      firstName
      lastName
      about
    }
  }
}
```