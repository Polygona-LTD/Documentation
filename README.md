# Polygona API

GraphQL API documentation for Polygona service.

### API Endpoint

```
https://polygona-service.nw.r.appspot.com/graphql
```

## Queries

### Fetch all products

```javascript
query products($consumerId: String!) {
  products(consumerId: $consumerId) {
    id
    slug
    name
    fileCount
    description
    publishedAt
    images {
        id
        url
    }
  }
}
```

Variables:

```javascript
{
  "consumerId": "string"
}
```

Example response:

```javascript
{
  "data": {
    "products": [
      {
        "id": "string",
        "slug": "string",
        "name": "string",
        "fileCount": "number",
        "description": "string"
        "publishedAt": "string"
        "images": [ {"id:" "string", "url": "string"}, ... ]
      }
    ]
  }
}
```

### Fetch single product

```javascript
query product($consumerId: String!, $slug: String!){
  product(consumerId: $consumerId, slug: $slug){
    id
    slug
    name
    fileCount
    description
    publishedAt
    images {
        id
        url
    }
  }
}
```

Variables:

```javascript
{
  "consumerId": "string",
  "slug": "string"
}
```

Example response:

```javascript
{
  "data": {
    "product": {
        "id": "string",
        "slug": "string",
        "name": "string",
        "fileCount": "number",
        "description": "string"
        "publishedAt": "string"
        "images": [ {"id:" "string", "url": "string"}, ... ]
      }
  }
}
```

# Polygona 3D Client

Polygona 3D Client is developed with React and GraphQL and can be embedded into any kind of web-app.

## Requirements

- [Node.js](https://nodejs.org) installed on your system.
- A valid `consumerId` provided by Polygona.

## Setup

- Install the library by running `npm i polygona-3d-client`
- Embed it into your application (React example)

```javascript
import * as React from 'react';
import * as ReactDOM from 'react-dom';

import { Polygona3DClient } from 'polygona-3d-client';

const App = () => {
  return (
    <div>
      <div style={{ position: 'relative', height: '95vh' }}>
        <Polygona3DClient
          consumerId={YOUR_CONSUMER_ID}
          slug={product.slug}
          colorScheme={COLOR_SCHEME}
          objectColor={HEX_COLOR}
        />
      </div>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById('root'));
```

### Theming

Available color schemes: `gray`, `red`, `orange`, `yellow`, `green`, `teal`, `blue`, `cyan`, `purple`, `pink`

## Example

```javascript
import * as React from 'react';
import * as ReactDOM from 'react-dom';

import { Polygona3DClient } from 'polygona-3d-client';

const App = () => {
  return (
    <div>
      <div style={{ position: 'relative', height: '95vh' }}>
        <Polygona3DClient
          consumerId="YOUR_CONSUMER_ID"
          slug="customizable-minimalistic-egg-box"
          colorScheme="purple"
          objectColor="#b99aff"
        />
      </div>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById('root'));
```

## Handling events

```javascript
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { Polygona3DClient } from '../dist';

const App = () => (
  <div>
    <div id="header" style={{ height: '64px', backgroundColor: '#32aaca' }} />
    <div style={{ position: 'relative', height: '93vh', overflow: 'hidden' }}>
      <Polygona3DClient
        consumerId="YOUR_CONSUMER_ID"
        slug="customizable-minimalistic-egg-box"
        colorScheme="blue"
        objectColor="#3182ce"
        // Get loaded product info
        onProductLoad={product => console.log(product)}
        // Get download file urls
        onRequestDownloadURL={fileUrls => console.log(fileUrls)}
      >
        {/* Insert your own custom button */}      
        <button style={{ height: '40px' }}>3D Print it</button>
      </Polygona3DClient>
    </div>
  </div>
);

ReactDOM.render(<App />, document.getElementById('root'));
```