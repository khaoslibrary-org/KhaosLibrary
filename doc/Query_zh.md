

提供两种搜索数据的方式，足够地去中心化和开放：

- 通过Arweave通用的搜索网关

- 通过Khaos Library专用的搜索网关 - Magical Index



## Arweave通用的搜索网关

这种方式可以根据数据中的tag， 以GraphQL的方式搜索。

### 网关列表

| 名称                    | 地址/地址列表                                                | 备注                                                         |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 官方网关                | http://arweave.net/graphql                                   | 不开源                                                       |
| AR.IO网关               | https://gateway-explorer.vercel.app/                         | 开源，支持self-host。<br />在列表中地址后加 /graphql 就是搜索网关 |
| Goldensky               | https://arweave-search.goldsky.com/graphql                   | 和Arweave团队合作的搜索引擎，支持更强大的搜索功能，比如模糊搜索。 |
| irys网关(原bundlr)      | https://devnet.irys.xyz/graphql<br />https://node1.irys.xyz/graphql<br />https://node2.irys.xyz/graphql | 原bundlr团队提供的搜索网关                                   |
| KNN3 arseeding indexing | https://knn3-gateway.knn3.xyz/arseeding/graphql              |                                                              |

### 搜索示例

注意，为了防止脏数据干扰，请指定Khaos Library的官方地址：`0G6nYuKqlMpp920MiTAviJUTEWPGRE4yYb6Fey1OGtY` 。

当有相同isbn和id (tag 中)的多个数据时，表示数据经过修正，以revision最新的为准。

#### 通过isbn搜索书籍信息


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



#### 通过书名搜索书籍信息


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



#### 通过作者搜索书籍信息

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

#### 通过其他标识搜索书籍信息

如果需要通过其他标识搜索，请参照https://github.com/khaoslibrary-org/KhaosLibrary/blob/main/doc/Model.md#identifier  一节中的标识。



#### 获得更详细信息

搜索结果示例：

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

想获得更详细信息，请将  "transactions"- "edges"  -  "node"-   "id"的value，拼接在任意网关域名之后，比如：

[https://arweave.net/m7qwCmGcT4aIS9JNqExzB5OMIXzHviXxmGe634dP4iw](https://arweave.net/m7qwCmGcT4aIS9JNqExzB5OMIXzHviXxmGe634dP4iw) 



#### 高级搜索

- [官方文档](https://gql-guide.vercel.app/)
- https://cookbook.ar-io.dev/guides/querying-arweave/search-indexing-service.html

## Magical Index

khaos library专用的搜索网关，只索引khaos library相关数据的搜索网关，提供更加专业和快速的搜索。

正在开发中，后续会开源并支持self-host。
