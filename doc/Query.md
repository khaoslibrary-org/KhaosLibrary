

There are two ways to search for data that are sufficiently decentralized and open:

- Through the Arweave generic search gateway

- Through the Khaos Library dedicated search gateway - Magical Index



## Arweave Generic Search Gateway

This way, you can search the data in GraphQL based on the tags in the data.

### Gateway List

| Provider                    | Address/Address List                                                | Comment                                                         |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Arweave                | http://arweave.net/graphql                                   | non-open source                                                       |
| AR.IO               | https://gateway-explorer.vercel.app/                         | Open source, self-host support.<br />Add /graphql to the address in the list is the search gateway. |
| Goldensky               | https://arweave-search.goldsky.com/graphql                   | A search engine in collaboration with the Arweave team that supports more powerful search features such as fuzzy search. |
| irys(former bundlr)      | https://devnet.irys.xyz/graphql<br />https://node1.irys.xyz/graphql<br />https://node2.irys.xyz/graphql |                                    |
| KNN3 arseeding indexing | https://knn3-gateway.knn3.xyz/arseeding/graphql              |                                                              |

### Search example

Note that to prevent interference with dirty data, specify the official address of the Khaos Library: `0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY` .

When there is more than one data with the same 'isbn' and 'id' (in the tag), it means that the data has been corrected, with the largest revision number prevailing.

#### Search book metadata by isbn

```graphql
query( $count: Int ){
    transactions(
      first: $count, 
      owners:"0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY"       
      tags: [
        {
          name: "isbn",
          values: "9788571642423"
        },
      ]
    ) {
      edges {
        node {
          id
          owner {
            address
          }
          data {
            size
          }
          block {
            height
            timestamp
          }
          tags {
            name,
            value
          }
        }
      }
    }
  }
```



#### Search book metadata by book name

```graphql
query( $count: Int ){
    transactions(
      first: $count, 
      owners:"0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY"
      tags: [
        {
          name: "name",
          values: "Palomar"
        },
      ]
    ) {
      edges {
        node {
          id
          owner {
            address
          }
          data {
            size
          }
          block {
            height
            timestamp
          }
          tags {
            name,
            value
          }
        }
      }
    }
  }
```



#### Search book metadata by author

```graphql
query( $count: Int ){
    transactions(
      first: $count, 
      owners:"0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY"
      tags: [
        {
          name: "author",
          values: "Italo Calvino"
        },
      ]
    ) {
      edges {
        node {
          id
          owner {
            address
          }
          data {
            size
          }
          block {
            height
            timestamp
          }
          tags {
            name,
            value
          }
        }
      }
    }
  }

```

#### Search book metadata by other identifiers

If you need to search by other identifiers, please refer to: https://github.com/khaoslibrary-org/KhaosLibrary/blob/main/doc/Model.md#identifier.


#### Get more details

Example of search results:

```graphql
{
  "data": {
    "transactions": {
      "edges": [
        {
          "node": {
            "id": "m7qwCmGcT4aIS9JNqExzB5OMIXzHviXxmGe634dP4iw",
            "owner": {
              "address": "0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY"
            },
            "data": {
              "size": "2383"
            },
            "block": {
              "height": 1282122,
              "timestamp": 1697375516
            },
            "tags": [
              {
                "name": "Content-Type",
                "value": "application/json"
              },
              {
                "name": "appName",
                "value": "KhaosLibrary"
              },
              {
                "name": "id",
                "value": "ErdvLFXLJps2"
              },
              {
                "name": "name",
                "value": "Cosmicômicas, As"
              },
              {
                "name": "author",
                "value": "Italo Calvino"
              },
              {
                "name": "revision",
                "value": "0"
              },
              {
                "name": "isbn",
                "value": "9788571642423"
              },
              {
                "name": "ISBN10",
                "value": "8571642427"
              },
              {
                "name": "OPENLIBRARY",
                "value": "/books/OL9162856M"
              },
              {
                "name": "GOODREADS",
                "value": "209701"
              },
              {
                "name": "LIBRARYTHING",
                "value": "23501"
              },
              {
                "name": "language",
                "value": "pt"
              },
              {
                "name": "publisher",
                "value": "Companhia das Letras"
              },
              {
                "name": "publishDate",
                "value": "2000"
              }
            ]
          }
        }
      ]
    }
  }
}
```

For more details, take the value of "transactions" - "edges" - "node" - "id" and splice it after any gateway domain, for example:
[https://arweave.net/m7qwCmGcT4aIS9JNqExzB5OMIXzHviXxmGe634dP4iw](https://arweave.net/m7qwCmGcT4aIS9JNqExzB5OMIXzHviXxmGe634dP4iw) 



#### Advanced search

- [Arweave graphql guide](https://gql-guide.vercel.app/)
- https://cookbook.ar-io.dev/guides/querying-arweave/search-indexing-service.html

## Magical Index

Khaos Library dedicated search gateway, only index Khaos Library related data , provide more professional and fast search.

Under development, will be open source and support self-host.
