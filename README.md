# Startup Planet

I built this small Node.js and Express API as part of Scrimba. It serves a dataset of startups as JSON and lets you filter the results by location, industry, funding status, and whether a startup has a minimum viable product (MVP).

## What I learned

- **Setting up an Express API.** I used ES modules to import my data and route handlers, and `res.json()` to send the results back to the client.
- **Using query and path parameters.** I read optional filters from `req.query` and applied them one at a time with `Array.filter()` so a request can combine several filters. I used `req.params` to look up a single field and value from the URL, like `/api/country/germany`.
- **Handling strings and booleans.** I used `toLowerCase()` on both sides of text comparisons so capitalization doesn't affect the results. I also learned that `false` arrives in the query string as text, so I used `JSON.parse()` to turn `"true"` and `"false"` into booleans before comparing them with the dataset.
- **Organizing routes and controllers.** I mounted an `express.Router()` at `/api` and moved the filtering into separate controllers. That kept `server.js` focused on starting the server and setting up middleware.
- **Handling errors and enabling CORS.** I returned a `400` for unsupported path search fields and a JSON `404` for unknown endpoints. I added CORS middleware so a frontend running on a different origin can call the API from the browser.

## Run it locally

```sh
npm ci
npm start
```

Open [http://localhost:8000/api](http://localhost:8000/api) to see the full dataset.

| Request | What it returns |
| --- | --- |
| `GET /api` | All startups |
| `GET /api?industry=ai&has_mvp=true` | AI startups that have an MVP |
| `GET /api?continent=europe&is_seeking_funding=false` | European startups that aren't seeking funding |
| `GET /api/country/germany` | Startups in Germany |

Query filters support `industry`, `country`, `continent`, `is_seeking_funding`, and `has_mvp`. Path filters support `country`, `continent`, and `industry`.
