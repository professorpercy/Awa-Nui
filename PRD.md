# AWA NUI — Product Requirements Document

## Vision

AWA NUI is a music discovery platform organised by space — where music came from, what it connects to. Every other platform sorts by time (recently played, new releases). AWA NUI sorts by geography and genre kinship, making the relationships between music visible as a living map.

---

## Core Concept

Each node is an album. Colour = genre. Position = geographic origin (country view) or genre cluster (genre view). Lines connect albums that share DNA (overlapping genres). The map is navigable — zoom, pan, click to explore.

---

## Two Gardens

### Personal Garden
Your own record collection as a constellation. You curate it — add albums, remove them, connect them. Persistent across sessions (requires account). Can be seeded by importing your Discogs collection.

### Global Garden
The collective map — every user's garden combined. The most-loved records surface. No account required to explore. Users can pull albums from the Global Garden into their Personal Garden.

---

## Views

### Genre View
Albums clustered by genre group. Six groups: Electronic, World, Jazz, Reggae, Soul, Experimental. Sub-genres pull albums toward the cluster centre. Lines connect albums sharing a sub-genre tag.

### Country View
Albums pinned to their geographic origin on a real world map. Zoom into a region to see its music more clearly. Colour = country cluster.

---

## Features

### Map & Navigation
- Force-directed graph rendered on HTML5 canvas via D3
- Zoom and pan freely
- Hover tooltip shows album + artist name
- Click a node to open the side panel
- Ticker bar at the bottom — scrolling strip of genre/country filters, click to highlight matching nodes
- "SHOW ALL" button to clear active filter
- Toggle between Genre View and Country View

### Country View Map
- Real world map underlay using TopoJSON world atlas
- Country borders rendered as subtle green outlines
- Node glow scales with zoom level — tighter at low zoom, fuller when zoomed in
- No country name labels (map is self-evident at zoom)

### Side Panel
- Opens from the right, shifts the canvas left
- Album media area: embeds YouTube video if a URL is provided, otherwise shows album cover image, otherwise shows animated vinyl
- "SEARCH ON YOUTUBE" button that opens a YouTube search for the album
- External link button (Bandcamp, Discogs, SoundCloud, etc.)
- Album title, artist, country, genre group
- Short description / blurb
- Genre tag chips
- Similar Albums — up to 4 albums sharing genres, clickable to navigate
- Comments section — leave notes on any album
- Add to My Garden button (Global Garden view)
- Delete from Garden button (Personal Garden view)

### Adding Albums
- Manual add form: title, artist, genres, country, link, YouTube URL, cover image, description
- Discogs collection import — enter Discogs username, scans entire public collection and imports as nodes
- New nodes immediately appear on the graph

### Boot Screen
- Single explanatory paragraph covering the concept, how it works, and both modes
- Two entry buttons: Personal Garden / Global Garden
- Global Garden marked as "no login required"

---

## Technical Stack (Current)

- Single HTML file (no build system)
- D3.js v7 for force simulation and zoom
- TopoJSON for world map rendering
- HTML5 Canvas 2D for all rendering
- Static `albums.json` as data source
- No backend, no persistence — all state is in-memory

---

## Feature Checklist

### Done
- [x] World map underlay in country view (TopoJSON country polygons)
- [x] Country view node positioning via equirectangular geo projection
- [x] Genre view force-directed clustering
- [x] Zoom-aware node glow (scales with zoom level)
- [x] Country name labels removed — clean map
- [x] Boot screen with updated descriptive text
- [x] "No login required" label on Global Garden button
- [x] Side panel with album info, genre chips, external link
- [x] Side panel similar albums section (up to 4, clickable)
- [x] Side panel comments section (in-memory)
- [x] Side panel YouTube embed (when specific URL is provided)
- [x] Side panel "SEARCH ON YOUTUBE" button (opens search in new tab)
- [x] Add album to Personal Garden from Global Garden
- [x] Delete album from Personal Garden
- [x] Manual add album form (with YouTube URL field)
- [x] Discogs collection import (scans all pages, rate-limited)
- [x] Ticker bar genre and country filters
- [x] Toggle between Personal and Global Garden
- [x] Toggle between Genre View and Country View

### Not Done
- [ ] Auto-embed YouTube video without a manually provided URL (requires YouTube Data API key)
- [ ] User accounts and authentication
- [ ] Persistent Personal Garden (survives page refresh — needs backend/localStorage)
- [ ] Persistent comments (needs backend)
- [ ] True Global Garden — collective data shared across all users (needs backend + database)
- [ ] Album search by text / artist name
- [ ] Most-loved albums surfacing (upvotes, play counts — needs backend)
- [ ] Mobile / touch support (pan and zoom on touchscreen)
- [ ] Album blurb / description auto-populated (e.g. from MusicBrainz or Last.fm API)
- [ ] Album cover art auto-fetched (e.g. from Cover Art Archive)
- [ ] Influence lines — manual or algorithmic connections between albums beyond shared genre
- [ ] User profile page showing their garden publicly
- [ ] Share a node / garden as a link
- [ ] Onboarding flow for new users
- [ ] Deploy to a public URL
