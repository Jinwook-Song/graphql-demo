# GraphQL Demo

| 프로젝트 기간 | 22.08.12 ~                |
| ------------- | ------------------------- |
| 프로젝트 목적 | GraphQL, Hasura, Graphile |
| Github        | ‣                         |

---

```tsx
GraphQL
API를 위한 쿼리 언어
GraphQL은 클라이언트가 필요한 것을 정확하게 요청할 수 있는 기능을 제공하며, 시간이 지남에 따라 API를 더 쉽게 발전시키고 강력한 개발자 도구를 활성화합니다.
https://graphql.org/

Graphile
PostgreSQL를 위한 확장 가능한 고성능 자동 GraphQL API
https://www.graphile.org/

Hasura
모든 데이터에 대한 즉각적인 GraphQL
Hasura는 신규 및 기존 데이터 소스에 대한 즉각적인 GraphQL 및 REST API를 제공합니다. Hasura를 데이터에 연결하고 1분 이내에 API를 받으세요.
https://hasura.io/
```

---

```tsx
Swapi-GraphQL

GraphiQL은 GraphQL 쿼리를 작성, 검증 및 테스트하기 위한 브라우저 내 도구입니다.

https://graphql.org/swapi-graphql
```

---

### Setup

`npm init -y`

`npm i apollo-server graphql`

Api 의 shape을 먼저 설명해야 함

```jsx
import { ApolloServer, gql } from 'apollo-server';

// Schema Definition Language
const typeDefs = gql`
  type Query {
    text: String
  }
`;

const server = new ApolloServer({ typeDefs });

server.listen().then(({ url }) => {
  console.log(`✅ Running on ${url}`);
});
```

---

Query & Mutation

```tsx
const typeDefs = gql`
  type User {
    id: ID!
    username: String!
    firstName: String!
    lastName: String
  }
  type Tweet {
    id: ID!
    text: String!
    author: User!
  }
  type Query {
    allTweets: [Tweet!]!
    tweet(id: ID!): Tweet
  }
  type Mutation {
    postTweet(text: String!, userId: ID!): Tweet!
    deleteTweet(id: ID!): Boolean!
  }
`;
// GET /api/v1/tweets
// POST DELETE PUT /api/v1/tweets
// GET /api/v1/tweet/:id
```

---

Resolvers

```tsx
resolver 함수는 데이터베이스에 액세스한 다음 데이터를 반환합니다.
```

// args는 GraphQL 쿼리의 필드에 제공된 인수입니다.
Query: {
human(obj, args, context, info) {
return context.db.loadHumanByID(args.id).then(
userData => new Human(userData)
)
}
}

```
https://graphql.org/learn/execution/#root-fields-resolvers
```
