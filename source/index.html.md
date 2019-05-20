---
title: API Reference

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - queries
  - mutations
  - pagination
  - filtering
  - types
  - scenarios
  - changelog

search: true
---

# Introduction

> **API endpoint**

```
https://api.elemez.com/graphql
```

> All queries executed against the api are sent as `POST` requests.  
> We recommend [Insomnia.rest](https://insomnia.rest) to exercise our API

Welcome to the Elemez API Documentation! You can use this API to fetch data from the Elemez system for use in your own applications.

The API uses [GraphQL](https://graphql.org) syntax.  
If you are unfamiliar with this type of API we recommend following the link to the [documentation](https://graphql.org).

### Legacy REST API
For our legacy REST api please visit [http://docs.elemez.com](http://docs.elemez.com) for details

## HTTP Request Endpoint

`POST https://api.elemez.com/graphql`

# Authentication

Elemez uses API keys to allow access to the API. You can find your personal API token from the World Settings in the [Elemez Portal](https://elemez.com/world/settings)

Elemez expects for the API key to be included in all API requests to the server in a header that looks like the following:

`token: your-api-token`

<aside class="notice">
You must replace <code>your-api-token</code> with your personal API key.
</aside>
