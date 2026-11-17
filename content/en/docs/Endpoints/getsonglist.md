---
title: "getSongList"
linkTitle: "getSongList [OS]"
categories:
  - Lists
OpenSubsonic:
  - Extension
description: >
  Returns a list of random, newest, highest rated etc. songs.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songLists` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

`http://your-server/rest/getSongList`

Song-level counterpart of [`getAlbumList2`](../getalbumlist2): the same parameters and list
types, applied to songs.

### Parameters

| Parameter | Req. | OpenS. | Default | Comment |
| --- | --- | --- | --- | --- |
| `type` | **Yes** | **Yes** | | The list type. Must be one of the following: `random`, `newest`, `highest`, `frequent`, `recent`, `alphabeticalByName`, `alphabeticalByArtist`, `starred`, `byYear`, `byGenre`. |
| `size` | No | **Yes** | 10 | The number of songs to return. Max 500. |
| `offset` | No | **Yes** | 0 | The list offset. Useful if you for example want to page through the list of newest songs. |
| `fromYear` | **Yes** (if `type` is `byYear`) | **Yes** | | The first year in the range. If `fromYear > toYear` a reverse chronological list is returned. |
| `toYear` | **Yes** (if `type` is `byYear`) | **Yes** | | The last year in the range. |
| `genre` | **Yes** (if `type` is `byGenre`) | **Yes** | | The name of the genre, e.g., "Rock". |

The list types have the same meaning as in [`getAlbumList2`](../getalbumlist2), applied to songs.
For `alphabeticalByArtist`, songs are sorted by artist name, then title.

If `type` is not one of the values listed above, the server returns an error with code `0`.

### Example

{{% alert color="primary" %}} `http://your-server/rest/getSongList.view?type=newest&size=2&u=demo&p=demo&v=1.16.1&c=AwesomeClientName&f=json` {{% /alert %}}

### Result

A [`subsonic-response`](../../responses/subsonic-response) element with a nested [`songList`](../../responses/songlist) element on success.

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
  "subsonic-response": {
    "status": "ok",
    "version": "1.16.1",
    "openSubsonic": true,
    "songList": {
      "song": [
        {
          "id": "300000116",
          "title": "Can I Help U?",
          "album": "Forget and Remember",
          "artist": "Comfort Fit",
          "duration": 225
        }
      ]
    }
  }
}
{{< /tab >}}
{{< tab header="OpenSubsonic" lang="xml">}}
<subsonic-response status="ok" version="1.16.1" openSubsonic="true">
  <songList>
    <song id="300000116" title="Can I Help U?" album="Forget and Remember" artist="Comfort Fit" duration="225"/>
  </songList>
</subsonic-response>
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `songList` | [`songList`](../../responses/songlist) | **Yes** | **Yes** | The song list |
