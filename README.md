# yoScriptTagCheck


```typescript

import { createClient, fetchExchange } from "urql";
import gql from "graphql-tag";

interface SCRIPTTAGCHECK {
    shop: string, 
    accessToken: number
}

export const getScriptTags = gql`
  query getScriptTags {
    scriptTags(first: 10) {
      edges {
        node {
          id
          src
        }
      }
    }
  }
`;

export const scriptTagCheck = async (scriptTagCheck:SCRIPTTAGCHECK) => {
    const client = createClient({
        url: `https://${scriptTagCheck.shop}/admin/api/2020-07/graphql.json`,
        fetchOptions: {
          headers: {
            "Content-Type": "application/json",
            "X-Shopify-Access-Token": scriptTagCheck.accessToken,
          },
        },
        requestPolicy: "network-only",
        exchanges: [fetchExchange]
    })

    const res = await client.query(getScriptTags).toPromise(); 

    return false;
}
