# Dota 2 Replay Analysis

Project-based approach to better improve my understanding and my utilization of GO as well as tieing in with something what I love doing on my free time. The plan is to build an analysis tool based on replay files that are available through OpenDota API and the analysis will be looking at your macro decisions rather your cognitive or motor skills because you really can't tell somebody that you could've react faster here but what you could tell is not to keep going to the same area that you died 30 seconds ago.

## What it looks at

- **Fight participation**: fights you could see and reach but didn't join
- **Deaths**: deaths with enemies missing from your map and no vision nearby
- **Post-fight conversion**: won fights that didn't turn into towers or Roshan
- **Item build**: timings and choices against benchmarks and the enemy lineup

Every finding comes with a timestamp, what to do instead, and a confidence level. It only uses information/vision available to your team, because I know in replays, fog doesn't exist unless like you toggle it on/off.

## Architecture

Three Go services, each owning its own store because why not lol:

- `api`: Steam sign-in, match list, reports (App DB, Postgres)
- `ingest`: downloads, caches and parses replays (S3)
- `analysis`: detects decision points and runs the analyzers (Game DB, Postgres)

I recently learned about Jev, so I wanted to test it and I plan to use it as the judge in my Dota 2 replay analyzer letting it decides whether it was a good call and what I should have done instead.

## Planned Stack

Go · gRPC/protobuf · PostgreSQL (pgx, sqlc) · Redis (asynq) · S3 · OpenTelemetry · Docker · [manta](https://github.com/dotabuff/manta) replay parser · OpenDota API · Jev (TypeSafe AI)
