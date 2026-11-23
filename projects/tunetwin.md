# TuneTwin

TuneTwin helps two listeners find shared music in their Spotify libraries and save a selection as a playlist. The app uses React and Vite on the frontend and Flask on the backend. [Visit TuneTwin](https://tunetw.in/)

## Showing matches during a scan

Reading saved tracks and playlists can take many requests. The comparison publishes matches in pages so listeners can start browsing while the scan continues. Each reader tracks its own position within a comparison run. A new run resets that position and clears the old results.

A lost response can be retried from the last accepted position. The client validates each page before advancing and merges matches by track ID so a repeated page preserves display order.

## Reporting progress

Early in a scan, the system may know how many saved tracks it has read while it is still counting playlist entries. The UI waits for a confirmed total before showing a coverage percentage. This avoids showing full coverage while part of the library is still being counted.

The code sample contains the page validation, track merge, and coverage logic, with regression tests and a demo that runs on synthetic data. [Run the comparison sample](https://github.com/beaubl/tunetwin-comparison-sample)
