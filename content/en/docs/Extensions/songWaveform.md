---
title: "Song waveform"
linkTitle: "Song waveform"
OpenSubsonic:
  - Extension
description: >
  Retrieve the loudness envelope of a song, for example to draw a waveform seek bar or plan crossfades.
---

**OpenSubsonic version**: [1](../../opensubsonic-versions)

**OpenSubsonic extension name** `songWaveform` (As returned by [`getOpenSubsonicExtensions`](../../endpoints/getopensubsonicextensions))

## Version 1

This extension requires the following endpoints:

- [`getWaveform`](../../endpoints/getwaveform): Fetch the loudness envelope of a song by id

The endpoint returns a [`waveform`](../../responses/waveform) element, which holds the RMS level of the song in dBFS, at a fixed base resolution of one value per 100 ms, optionally reduced to a requested number of values.
