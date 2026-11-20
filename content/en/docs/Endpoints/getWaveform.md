---
title: "getWaveform"
linkTitle: "getWaveform [OS]"
OpenSubsonic:
  - Extension
categories:
  - Media retrieval
description: >
  Returns the loudness envelope of a song.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songWaveform` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

`http://your-server/rest/getWaveform`

Returns the loudness envelope of a song. Clients can use it to draw a waveform, for example behind the seek bar, or to plan crossfades.

Servers store the envelope at a fixed base resolution of one value per 100 ms. Value `i` is the RMS level, in dBFS, of the audio from `i × 100` ms to `(i + 1) × 100` ms, with all channels combined. The last value covers whatever audio is left, which can be shorter than 100 ms. A song of `duration` seconds therefore has `N = ceil(duration × 10)` base values. Because the resolution and the scale are fixed, values can be cached and compared between songs and between servers.

Levels are in dBFS (decibels relative to full scale), rounded to 2 decimal places, from `-120` to `0`. `0` is a full-scale signal, and `-120` is silence: servers clamp any lower level, including digital silence, to `-120`.

Without `samples`, the server returns all `N` base values. With `samples`, the server reduces the base values to exactly `samples` values: value `i` covers the base values from `floor(i × N / samples)` to `floor((i + 1) × N / samples) - 1`, and is the highest of them, so short loud parts stay visible. If `samples` is greater than or equal to `N`, the server returns the `N` base values unchanged. This is the only case where the response holds fewer values than requested.

Servers may compute waveforms on demand, so the first request for a song can take longer than later ones. A server that advertises the extension but cannot produce a waveform for a song (for example because waveforms are turned off) returns a regular [`error`](../../responses/error).

### Parameters

| Parameter | Req. | OpenS. | Default | Comment |
| --- | --- | --- | --- | --- |
| `id` | **Yes** | **Yes** | | The ID of the song. |
| `samples` | No | **Yes** | | The number of values to return. Must be a positive integer. If omitted, the server returns all base values (one per 100 ms). If greater than or equal to the number of base values, the server returns all base values. |

### Example

{{< alert color="primary" >}} `http://your-server/rest/getWaveform.view?id=300000060&samples=8&u=demo&p=demo&v=1.16.1&c=AwesomeClientName&f=json` {{< /alert >}}

### Result

A [`subsonic-response`](../../responses/subsonic-response) element with a nested [`waveform`](../../responses/waveform) element on success.

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
  "subsonic-response": {
    "status": "ok",
    "version": "1.16.1",
    "type": "AwesomeServerName",
    "serverVersion": "0.1.3 (tag)",
    "openSubsonic": true,
    "waveform": {
      "id": "300000060",
      "duration": 304.5,
      "interval": 38062.5,
      "samples": 8,
      "levels": [-31.42, -14.05, -9.87, -6.12, -7.3, -10.56, -17.91, -48.2]
    }
  }
}
{{< /tab >}}
{{< tab header="Subsonic" lang="json" >}}
Does not exist.
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `waveform` | [`waveform`](../../responses/waveform) | **Yes** | **Yes** | The loudness envelope of the song. |
