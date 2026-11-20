---
title: "waveform"
linkTitle: "waveform [OS]"
OpenSubsonic:
  - Addition
description: >
  The loudness envelope of a song.
---

{{< tabpane persist=false >}}
{{< tab header="**Example**:" disabled=true />}}
{{< tab header="OpenSubsonic" lang="json">}}
{
  "id": "300000060",
  "duration": 304.5,
  "interval": 38062.5,
  "samples": 8,
  "levels": [-31.42, -14.05, -9.87, -6.12, -7.3, -10.56, -17.91, -48.2]
}
{{< /tab >}}
{{< tab header="Subsonic" lang="json" >}}
Does not exist.
{{< /tab >}}
{{< /tabpane >}}

| Field | Type | Req. | OpenS. | Details |
| --- | --- | --- | --- | --- |
| `id` | `string` | **Yes** | **Yes** | The ID of the song. |
| `duration` | `number` | **Yes** | **Yes** | The duration of the song in seconds. |
| `interval` | `number` | **Yes** | **Yes** | The length of audio, in milliseconds, that each value of `levels` covers: `100` for the base resolution, or `100 × N / samples` after reduction, where `N` is the number of base values. Value `i` starts at about `i × interval` ms. |
| `samples` | `int` | **Yes** | **Yes** | The number of values in `levels`. This is lower than the requested number of samples only when the request asks for more values than the base resolution holds. |
| `levels` | Array of `number` | **Yes** | **Yes** | One RMS level per slice of the song, in playback order, in dBFS rounded to 2 decimal places, from `-120` (silence) to `0` (full scale). After reduction, each value is the highest base value of its slice. See [`getWaveform`](../../endpoints/getwaveform) for how the values are computed. |

In XML, each value of `levels` is a separate `<levels>` child element of `<waveform>`, in order.
