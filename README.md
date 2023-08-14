# Theatre.js Continuous Keyframes

This repository contains a testbed to experiment with Theatre.js' ability to continuously record keyframes.

Relevant files:

- /src/lib/components/Recorder.svelte

## Install

```bash
pnpm i
```

## Run

```bash
pnpm dev
```

## Usage

1. Open the app in a browser
2. Press "r" to start recording

- This will add a `studio.transaction` and advance the `sheet.sequence`

3. Press "r" again to stop recording

## Expected Behavior

The `sheet.sequence` should advance continuously while recording without hiccups. A keyframe should be added to the sequence every frame.

## Actual Behavior

The `sheet.sequence` does not advance continuously while recording. On a 2019 Macbook Pro 16", Google Chrome will throw these warnings:

```
[Violation] 'requestAnimationFrame' handler took 97ms
```

The hiccups eventually cause a complete standstill of the UI.
