# Star Wars GQL API

This GraphQL API retrieves all the Star Wars data you've ever wanted: Planets, Spaceships, Vehicles, People, Films and Species from all seven Star Wars films. 

It is publicly hosted [here](https://swapi-graphql.netlify.app/.netlify/functions/index), but by using this API example in Tyk you'll be able to:

- quickly get going with your first protected GQL API
- automatically generate authorization token while creating the example and use it immediately to access the API
- get to know how Tyk's raw API definition looks like for GQL APIs

It's a great starting point!

## What will happen after you click "Use example" button?

- You'll see `Star Wars API` in your list of APIs
- You'll also get a nice green pop-up with an authorization key - copy that, you'll need it!

## Try it out!

To try out this API you need 2 things:

- your authorization key you got from that pop-up, that you should have saved somewhere
- your first GQL query

### Step-by-step instructions

1. Navigate to "Playground" tab in the Dashboard
2. Find `Request headers` section at the bottom and expand it
3. Paste this in there:

```json
{
  "Authorization": "<YOUR-AUTHORIZATION KEY>"
}
```

4. At the top of the GQL Playground paste your first query:

```graphql
query myFirstQuery {
  allFilms {
    films {
      title
      director
      releaseDate
      speciesConnection {
        species {
          name
          classification
          homeworld {
            name
          }
        }
      }
    }
  }
}
```

5. Click the `PLAY` button at the top and wait for the response to populate on the right-hand side!

Now go and try writing your own query!