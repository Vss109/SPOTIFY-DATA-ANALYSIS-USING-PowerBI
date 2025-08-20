# SPOTIFY-DATA-ANALYSIS-USING-PowerBI
data analysis on spotify music trends using powerbi
📌 Overview

This project explores Spotify listening behavior and music trends using an interactive Power BI dashboard. It highlights:

Who we listen to: Top artists, albums, and tracks

When we listen: Day & hour patterns

How preferences evolve: Year-over-year trends

What we like: Audio features (danceability, energy, tempo, valence, etc.)

🧩 Key Features

Overview: KPIs (total tracks, artists, albums) with YoY comparisons

Listening Patterns:

Heatmap of hour vs day listening peaks

Track frequency vs avg listening time (engagement)

Filters for year, platform, shuffle/skip behavior

Details:

Top artists/albums/tracks with rankings

Trends from 2014–2024

Quick comparisons vs previous period

Interactivity: Slicers for Year, Platform (Android/iOS/Web/Desktop), Genre, Artist


🧱 Data Model

A simple star-schema:

Fact: FactListening (plays, duration, timestamps, platform, shuffle/skip flags, track_id)

Dimensions: DimTrack, DimArtist, DimAlbum, DimDate, DimPlatform, DimGenre

Relationships:
FactListening[track_id] → DimTrack[track_id]
DimTrack[artist_id] → DimArtist[artist_id]
DimTrack[album_id] → DimAlbum[album_id]
FactListening[date] → DimDate[date]
FactListening[platform_id] → DimPlatform[platform_id]

🔧 Data Preparation (Power Query)

Removed duplicates & null rows

Standardized column types (dates, durations, booleans)

Extracted Hour, Day Name, Month, Year from timestamps

Normalized text (trim, lowercase for joins)

Built a Date table (calendar) for time intelligence

📊 Sample DAX Measures
Total Plays = COUNTROWS(FactListening)

Total Listening Minutes = 
DIVIDE(SUM(FactListening[duration_ms]), 60000)

Avg Listening Time (sec) =
DIVIDE(SUM(FactListening[duration_ms]), COUNTROWS(FactListening)) / 1000

Tracks (Distinct) = DISTINCTCOUNT(FactListening[track_id])
Artists (Distinct) = DISTINCTCOUNT(DimArtist[artist_id])
Albums (Distinct) = DISTINCTCOUNT(DimAlbum[album_id])

YoY Plays % =
VAR Curr = [Total Plays]
VAR Prev = CALCULATE([Total Plays], DATEADD(DimDate[date], -1, YEAR))
RETURN DIVIDE(Curr - Prev, Prev)

Track Rank by Plays =
RANKX(ALL(DimTrack[track_name]), [Total Plays], , DESC)

🔍 Insights (Example Highlights)

Evening peaks between 6–11 PM; weekend listening is higher

A few artists dominate plays; long tail of tracks with short durations

Noticeable YoY fluctuations—recent year shows decline in unique artists/albums (sample dependent)

Your insights will vary based on your dataset—update this section with findings from your report.

▶️ How to Open / Use

Download pbix/Spotify_TuneTrends.pbix

Open in Power BI Desktop (latest)

Replace data source paths (if prompted)

Refresh to load visuals

Optional (Publish/Embed):

Publish to Power BI Service → File > Publish to web → get public link/iframe for your portfolio

🔗 Dataset

Source: (Add link or mention “personal export / academic dataset / Kaggle link”)

Columns used (typical): track, artist, album, played_at, duration_ms, platform, is_shuffle, is_skipped, danceability, energy, tempo, valence, genre

🚀 Future Improvements

Add sessionization (continuous listening sessions)

Cohort analysis for returning vs new artists

Audio feature clustering (k-means) for playlist recommendations

Incremental refresh / parameterized data source

Deploy with Power BI App for polished distribution

🛠 Skills Demonstrated

Power BI, Power Query (ETL), DAX, Data Modeling (Star Schema), Time Intelligence, Interactive Dashboards, KPI Design, Trend & Behavioral Analysis, Storytelling with Data
