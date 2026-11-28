---
title: "UpdateCollectionRequest"
linkTitle: "UpdateCollectionRequest [OS]"
categories:
- Collections
opensubsonic:
- Extension
description: >
  Request payload for updating a collection.
---

Should be used in the [UpdateCollection](../endpoints/updatecollection) endpoint.
Only the fields supplied in the request payload will have an effect on a collection.

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="Name and comment" lang="json">}}
{
  "collectionId": "23785995",
  "name": "new name",
  "comment": "this is a new comment"
}
{{< /tab >}}
{{< tab header="Set items" lang="json">}}
{
  "collectionId": "23785995",
  "setItems": [
    {
      "type": "song",
      "id": "300000060"
    },
    {
      "type": "album",
      "id": "200000021"
    },
    {
      "type": "genre",
      "id": "vaporwave"
    }
  ]
}
{{< /tab >}}
{{< tab header="Add items" lang="json">}}
{
  "collectionId": "23785995",
  "addItems": {
    "items": [
      {
        "type": "album",
        "id": "1234"
      }
    ],
    "to": 6
  }
}
{{< /tab >}}
{{< tab header="Move items" lang="json">}}
{
  "collectionId": "23785995",
  "moveItems": {
    "fromStart": 0,
    "fromEnd": 5,
    "to": 20
  }
}
{{< /tab >}}
{{< tab header="Remove items" lang="json">}}
{
  "collectionId": "23785995",
  "removeItems": [0, 1, 2, 6]
}
{{< /tab >}}
{{< /tabpane >}}

| Field |  Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `collectionId` | string | **Yes** | **Yes** | The collection ID. |
| `name` | string | No | **Yes** | The human-readable name of the collection. Cannot be an empty string. |
| `comment` | string | No | **Yes** | The collection comment. |
| `public` | boolean | No | **Yes** | `true` if the collection should be visible to all users, `false` otherwise. |
| `setItems` | [CollectionItemID[]](../payloads/collectionitemid) | No | **Yes** | Replace the list of items with the ones provided. Each item must occur at most once. |
| `addItems` | [AddItemsToCollection](../payloads/additemstocollection) | No | **Yes** | Add items to the collection. |
| `moveItems` | [MoveRange](../payloads/moverange) | No | **Yes** | Move items from the original position to another in the collection. |
| `removeItesm` | Array of integer | No | **Yes** | Remove the items at the specified positions from the collection. |

Only one of `setItems`, `addItems`, `moveItems`, and `removeItems` can be non-empty in a single request.
