---
title: "Song lists"
linkTitle: "Song lists"
OpenSubsonic:
  - Extension
description: >
  Adds support for retrieving lists of songs analogous to album lists.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songLists` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

When a server supports this extension, it provides the new endpoint [`getSongList`](../../endpoints/getsonglist).

## Version 1

[`getSongList`](../../endpoints/getsonglist) is a thin, song-level version of
[`getAlbumList2`](../../endpoints/getalbumlist2): the same parameters, list types and paging
semantics, returning `Child` entries instead of albums. It adds no new parameters or response
fields. Servers MUST support all list types listed in `getSongList`.
