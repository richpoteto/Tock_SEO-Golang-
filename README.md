
# SEO

<p align="center">
<img src="docs/pics/logo_200.png" alt="SEO" title="SEO" />
</p>



SEO is a dynamic renderer to provide zero-configuration server-side rendering mainly to web crawlers in order to effortlessly improve SEO for websites developed in modern Javascript frameworks such as React.js, Vue.js, Angular.js, etc... SEO works totally independently of your frontend and backend stacks

<p align="center">
<img src="docs/pics/diagram.png" alt="SEO's Diagram" title="SEO's Diagram" />
</p>

## Main Features
* Zero change needed in frontend and backend code
* Filters based on user agents and paths
* Single fast binary written in Golang
* Multiple Caching strategies
* Support for asynchronous pages
* Prometheus metrics
* Choose your configuration system (YAML, TOML or JSON)
* Container ready

## How does SEO work?

This program is listening by default to the port `3001` but can be changed using the config file; for every request coming from the frontend server or the outside world, there are some checks or filters that are tested against the headers and/or paths according to SEO's configuration file to determine whether SEO should just pass the initial HTML returned from the backend server or use headless Chrome to provide a server-side rendered HTML. To be more specific, for every request there are 2 paths:

1. If the request is whitelisted as a candidate for SSR (i.e. a GET request that passes all user agent and path filters), SEO instructs the headless Chrome instance to request the corresponding page, render it and return the response which contains the final server-side rendered HTML. You usually want to whitelist only web crawlers like GoogleBot, BingBot, etc...

2. If the request isn't whitelisted (i.e. the request is not a GET request or doesn't pass any of the filters), SEO will simply act as a transparent reverse HTTP proxy and just conveys requests and responses as they are. You usually want to blacklist real users in order to return the usual client-side rendered HTML coming from the backend server back to them.
