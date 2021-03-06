# Node.js API Starter Kit &nbsp; <a href="https://gitter.im/kriasoft/nodejs-api-starter"><img src="https://img.shields.io/gitter/room/kriasoft/nodejs-api-starter.js.svg" width="102" height="20"></a> <a href="https://github.com/kriasoft/nodejs-api-starter/stargazers"><img src="https://img.shields.io/github/stars/kriasoft/nodejs-api-starter.svg?style=social&label=Star&maxAge=3600" height="20"></a> <a href="https://twitter.com/ReactStarter"><img src="https://img.shields.io/twitter/follow/ReactStarter.svg?style=social&label=Follow&maxAge=3600" height="20"></a>

[Node.js API Starter Kit][nodejskit] is a boilerplate and tooling for authoring **data API**
backends with [Node.js][node], [JavaScript][js] (via [Babel][babel]) and [GraphQL][gql]. It's
meant to be paired with a web and/or mobile application project such as [React Starter Kit][rsk].

#### This project is maintained with support from <a href="https://rollbar.com/?utm_source=reactstartkit(github)&utm_medium=link&utm_campaign=reactstartkit(github)"><img src="https://koistya.github.io/files/rollbar-247x48.png" height="24" align="top" /></a> <a href="https://x-team.com/?utm_source=reactstarterkit&utm_medium=github-link&utm_campaign=reactstarterkit-june"><img src="https://koistya.github.io/files/xteam-168x48.png" height="24" align="top" /></a><sup><a href="https://x-team.com/join/?utm_source=reactstarterkit&utm_medium=github-link&utm_campaign=reactstarterkit-june">Hiring</a></sup>


## Features

✓ Cross-platform development on macOS, Windows or Linux inside [Docker][docker], single dev dependency<br>
✓ [GraphQL][gql] boilerplate, everything needed to get started building a [GraphQL][gql] API endpoint / gateway<br>
✓ [PostgreSQL][pg] database schema boilerplate and migration tools (see [`tools`](./tools), [`migrations`](./migrations))<br>
✓ Authentication and authorization via [Passport.js][passport] (see [`src/passport.js`](./src/passport.js), [`src/routes/account.js`](./src/routes/account.js))<br>
✓ Session and cache management with [Redis][redis] and [DataLoader][loader] (see [stop using JWT for sessions](http://cryto.net/~joepie91/blog/2016/06/13/stop-using-jwt-for-sessions/))<br>
✓ **24/7** community support on [Gitter][gitter] + *premium support* on [Skype][skype] ([book a session](https://calendly.com/koistya))<br>


## Directory Layout

```bash
.
├── /build/                     # The compiled output (via Babel)
├── /config/                    # Configuration files (for Docker containers etc.)
├── /locales/                   # Localization resources (i18n)
├── /migrations/                # Database schema migrations
├── /seeds/                     # Scripts with reference/sample data
├── /src/                       # Node.js application source files
│   ├── /emails/                # Handlebar templates for sending transactional email
│   ├── /mutations/             # GraphQL mutations, e.g. createStory(), updateStory()
│   ├── /routes/                # Express routes, e.g. /login/facebook
│   ├── /types/                 # GraphQL types with resolve functions
│   │   ├── /Node.js            # Relay's "node" definitions
│   │   ├── /UserType.js        # User account (id, email, etc.)
│   │   └── /...                # etc.
│   ├── /app.js                 # Express.js application
│   ├── /DataLoader.js          # Data access utility for GraphQL /w batching and caching
│   ├── /db.js                  # Database access and connection pooling (via Knex)
│   ├── /email.js               # Client utility for sending transactional email
│   ├── /passport.js            # Passport.js authentication strategies
│   ├── /redis.js               # Redis client
│   ├── /schema.js              # GraphQL schema
│   └── /server.js              # Node.js server (entry point)
├── /test/                      # Unit, integration and load tests
├── /tools/                     # Build automation scripts and utilities
├── docker-compose.yml          # Defines Docker services, networks and volumes
├── Dockerfile                  # Commands for building a Docker image for production
├── package.json                # The list of project dependencies
└── yarn.lock                   # Fixed versions of all the dependencies
```


## Getting Started

Make sure that you have [Docker][docker] v17 or newer installed plus a good text editor or IDE
([VS Code][code], [WebStorm][wstorm] or another), clone the repo and launch the app with [Docker
Compose][compose]:

```bash
git clone -o nodejs-api-starter -b master --single-branch \
   https://github.com/kriasoft/nodejs-api-starter.git example-api
cd example-api                  # Change current directory to the newly created one
docker-compose up               # Launch Docker containers with the Node.js API app running inside
```

The API server must become available at [http://localhost:8080/graphql](http://localhost:8080/graphql)
([live demo][demo]).

Once the docker container named `api` is started, the Docker engine executes `node tools/run.js`
command that installs Node.js dependencies, migrates database schema to the latest version,
compiles Node.js app from source files (see [`src`](./src)) and launches it with "live reload"
on port `8080`.

In order to open a new terminal session from inside the `api` Docker container run:

```bash
docker-compose exec api /bin/sh
```

From this shell you can run automation scripts such as `yarn test`, `yarn run db:migrate` etc.
Find the full list of scripts available inside the [`tools`](./tools) folder and
the [`package.json`](./package.json) file.

In order to open a postgres shell, run the following:

```bash
docker-compose exec db psql -U postgres
```

## Testing

```bash
yarn run lint                   # Find problematic patterns in code
yarn run check                  # Check source code for type errors
yarn run test                   # Run unit tests once
yarn run test:watch             # Run unit tests in watch mode
```


## Debugging

In order to run the app with [V8 inspector][v8debug] enabled, simply replace `node tools/run.js`
with `node --inspect tools/run.js` in either [`docker-compose.yml`](docker-compose.yml) file, or
even better in `docker-compose.override.yml`. Then restart the app (`docker-compose up`) and
[attach your debugger][vsdebug] to `127.0.0.1:9230` (see [`.vscode/launch.json`](https://gist.github.com/koistya/421ea3e0139225b27f909e98202a34de)
for [VS Code][code] as an example).


## Keeping Up-to-Date

If you keep the original Git history after clonning this repo, you can always fetch and merge
the recent updates back into your project by running:

```bash
git checkout master
git fetch nodejs-api-starter
git merge nodejs-api-starter/master
docker-compose up
```


## Deployment

Customize the deployment script found in `tools/publish.js` if needed. Then whenever you need to
deploy your app to a remote server simply run:

```bash
node tools/publish <host>       # where <host> is the name of your web server (see ~/.ssh/config)
```

Not sure where to deploy your app? [DigitalOcean][do] is a great choice in many cases (get [$10 credit][do])


## Contributing

Anyone and everyone is welcome to [contribute](CONTRIBUTING.md). Start by checking out the list of
[open issues](https://github.com/kriasoft/nodejs-api-starter/issues) marked
[help wanted](https://github.com/kriasoft/nodejs-api-starter/issues?q=label:"help+wanted").
However, if you decide to get involved, please take a moment to review the [guidelines](CONTRIBUTING.md).


## Books and Tutorials

[![Docker in Action](https://images-na.ssl-images-amazon.com/images/I/518L63vGMpL._SL160_.jpg)](http://amzn.to/2hmUrNP)
[![You Don't Know JS](https://images-na.ssl-images-amazon.com/images/I/B172ZcXnYDS._SL160_.png)](http://amzn.to/2idQ3gL)
[![JavaScript Ninja](https://images-na.ssl-images-amazon.com/images/I/51tQ+JAczgL._SL160_.jpg)](http://amzn.to/2idDamK)
[![Effective JavaScript](https://images-na.ssl-images-amazon.com/images/I/51W25NBDLQL._SL160_.jpg)](http://amzn.to/2idMZBq)
[![NodeSchool.io](http://koistya.github.io/files/nodeschool.jpg)](https://nodeschool.io/)

## Related Projects

* [GraphQL.js](https://github.com/graphql/graphql-js) — The JavaScript reference implementation for [GraphQL](http://graphql.org/)
* [DataLoader](https://github.com/facebook/dataloader) — Batching and caching for GraphQL data access layer
* [React Starter Kit](https://github.com/kriasoft/react-starter-kit) — Isomorphic web app boilerplate (React, Node.js, Babel, Webpack, CSS Modules)
* [React Static Boilerplate](https://github.com/kriasoft/react-static-boilerplate) — Single-page application (SPA) starter kit (React, Redux, Webpack, Firebase)
* [Membership Database](https://github.com/membership/membership.db) — SQL schema boilerplate for user accounts, profiles, roles, and auth claims


## Support

* [#nodejs-api-starter](https://gitter.im/kriasoft/nodejs-api-starter) on Gitter — Watch announcements, share ideas and feedback
* [GitHub Issues](https://github.com/kriasoft/nodejs-api-starter/issues) — Check open issues, send bug reports feature requests
* [@koistya](https://twitter.com/koistya) on [Codementor](https://www.codementor.io/koistya) or [Skype][skype] — Private consulting and customization requests


## License

Copyright © 2016-present Kriasoft. This source code is licensed under the MIT license found in the
[LICENSE.txt](https://github.com/kriasoft/nodejs-api-starter/blob/master/LICENSE.txt) file.

---
Made with ♥ by Konstantin Tarkus ([@koistya](https://twitter.com/koistya), [blog](https://medium.com/@tarkus)) and [contributors](https://github.com/kriasoft/nodejs-api-starter/graphs/contributors)


[nodejskit]: https://github.com/kriasoft/nodejs-api-starter
[rsk]: https://github.com/kriasoft/react-starter-kit
[node]: https://nodejs.org
[js]: https://developer.mozilla.org/docs/Web/JavaScript
[babel]: http://babeljs.io/
[gql]: http://graphql.org/
[yarn]: https://yarnpkg.com
[demo]: https://reactstarter.com/graphql
[pg]: https://www.postgresql.org/
[do]: https://m.do.co/c/eef302dbae9f
[code]: https://code.visualstudio.com/
[wstorm]: https://www.jetbrains.com/webstorm/
[docker]: https://www.docker.com/community-edition
[compose]: https://docs.docker.com/compose/
[v8debug]: https://chromedevtools.github.io/debugger-protocol-viewer/v8/
[vsdebug]: https://code.visualstudio.com/Docs/editor/debugging
[passport]: http://passportjs.org/
[redis]: https://redis.io/
[loader]: https://github.com/facebook/dataloader
[gitter]: https://gitter.im/kriasoft/nodejs-api-starter
[skype]: https://calendly.com/koistya
