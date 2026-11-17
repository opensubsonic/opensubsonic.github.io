---
title: "songList"
linkTitle: "songList [OS]"
OpenSubsonic:
  - Extension
description: >
  Song list.
---

Song-level version of [`albumList2`](../albumlist2): [`Child`](../child) entries instead of albums.

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
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
{{< /tab >}}
{{< tab header="OpenSubsonic" lang="xml">}}
<songList>
  <song id="300000116" title="Can I Help U?" album="Forget and Remember" artist="Comfort Fit" duration="225"/>
</songList>
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `song` | Array of [`Child`](../child) | No | | The songs |
