# channels-and-epg

[![Last commit](https://img.shields.io/github/last-commit/crisvale/channels-and-epg?style=flat-square)](https://github.com/crisvale/channels-and-epg/commits/main)
[![Repo size](https://img.shields.io/github/repo-size/crisvale/channels-and-epg?style=flat-square)](https://github.com/crisvale/channels-and-epg)

Automated, consolidated XMLTV guides by country, plus channel catalogs by operator. Updated three times per day.

## Features

- One unified XMLTV guide per country.
- Channels deduplicated across operators.
- Best data source selected per time slot.
- Enriched metadata via TMDB when available.
- Gzip-compressed for efficient delivery.
- Smart updates: only changed files are published.

## XMLTV Guides

Each country has a single XMLTV file combining all supported operators.

| Country | File | Channels | Operators |
| --- | --- | ---: | --- |
| France | `epg/france.xml.gz` | 659 | Canal+, Orange, SFR |
| United Kingdom | `epg/united-kingdom.xml.gz` | 535 | Freeview, Freesat, Sky UK, Virgin TV Go |
| Germany | `epg/germany.xml.gz` | 490 | Magenta TV, Sky DE |
| Congo | `epg/congo.xml.gz` | 355 | Canal+ Congo |
| Spain | `epg/spain.xml.gz` | 509 | Tivify, RTVE, Orange, Movistar Plus+, Atresplayer |
| Poland | `epg/poland.xml.gz` | 272 | Canal+ Poland, Polsat |
| Portugal | `epg/portugal.xml.gz` | 256 | MEO, NOS |
| Italy | `epg/italy.xml.gz` | 161 | Sky IT, RaiPlay, Tivu |

- Coverage: **7 days of programming**
- Format: XMLTV (`.xml.gz`)

### Usage

Most IPTV and media clients support direct XMLTV URLs, including Jellyfin, Emby, Plex, Tvheadend, and Kodi.

Example:

```bash
https://raw.githubusercontent.com/crisvale/channels-and-epg/main/epg/spain.xml.gz
```

If your client does not support gzip:

```bash
curl -sL https://raw.githubusercontent.com/crisvale/channels-and-epg/main/epg/spain.xml.gz | gunzip > spain.xml
```

### Program Metadata

Depending on availability from the source and TMDB, entries may include:

- Title and description, with the season and episode number folded into the title for series (for example, "NCIS - 21x09 Prime Cut").
- Poster or image.
- Year and category.
- Age rating.
- Cast and crew.
- Country of production.

Additional behavior:

- Titles and descriptions are published in the country's language.
- Programs spanning midnight are preserved as a single entry.
- Fragmented schedules, such as 5-minute blocks, are merged for readability.

## Channel Catalogs

Per-operator channel listings are provided in Markdown format.

- Each file includes logo, name, and channel number.
- Each catalog preserves the original naming and numbering used by the operator.
- Unlike the XMLTV guides, these catalogs are not unified across operators.
- Grouped one folder per country, matching the country XMLTV guide it feeds into.

```text
channels/spain/atresplayer.md         channels/italy/tivu.md
channels/spain/movistar.md            channels/united-kingdom/freesat.md
channels/spain/orange.md              channels/united-kingdom/freeview.md
channels/spain/rtve.md                channels/united-kingdom/sky-uk.md
channels/spain/tivify.md              channels/united-kingdom/virgin-uk.md
channels/france/canalplus.md          channels/portugal/meo.md
channels/france/orange-fr.md          channels/portugal/nos.md
channels/france/sfr.md                channels/congo/canalplus-cg.md
channels/germany/magenta-de.md        channels/poland/canalplus-pl.md
channels/germany/sky-de.md            channels/poland/polsat.md
channels/italy/raiplay.md
channels/italy/sky-it.md
```

## Update Schedule

All times are in Europe/Madrid.

| Time | Scope |
| --- | --- |
| 01:00 | Full 7-day refresh |
| 09:00 | Current day only |
| 18:00 | Next 3 days |

Behavior:

- Only the current day's schedule changes frequently.
- Future days usually remain unchanged once already published.
- A file is uploaded only if its content changed, keeping commit history meaningful.

## Data Sources

The guide data comes from public operator EPG sources and is enriched with metadata from [TMDB](https://www.themoviedb.org/).

This product uses the TMDB API but is not endorsed or certified by TMDB.

## Disclaimer

Files are provided as-is for personal use.

If you are a rights holder and want referenced content removed, please open an issue in the repository.
