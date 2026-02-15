# Plan My Ride - Equestrian Events Aggregator

> **Portfolio Project** | Aggregates unaffiliated UK horse events from multiple entry systems into one searchable calendar.

**[🌐 Live site: planmyride.co.uk](https://planmyride.co.uk)**

Closed-source; codebase in Azure DevOps. Showcased here to demonstrate technical capabilities.

---

## ⚡ At a glance

| | |
|---|---|
| **Live app** | [planmyride.co.uk](https://planmyride.co.uk) |
| **Stack** | C# / .NET 10 · Blazor WebAssembly (SPA) · Azure Functions · Azure Blob Storage |
| **What it does** | 9 UK horse-event sites → nightly multithreaded scrape (~10k events, ~3 mins) → JSON in blob → single calendar with postcode distance, filters, favorites |
| **Skills** | Full-stack .NET, Azure, web scraping, geospatial (Haversine, geocoding), client-side performance, unit tests, clean architecture |

**Jump:** [Architecture](#-architecture) · [Features](#-features) · [Tech](#-tech--tools) · [Future](#-future)

---

## 🎯 Overview

One place to find unaffiliated equestrian events: **9 sources**, **~10,000 events** scraped nightly in **~3 minutes** (multithreaded). Client-side filtering, distance-from-postcode sorting, favorites, responsive UI.

---

## 🌐 Event sources (9 sites)

| Site | URL |
|------|-----|
| EQ Events | [equoevents.co.uk](https://www.equoevents.co.uk) |
| Horse-Events | [horse-events.co.uk](https://www.horse-events.co.uk) |
| Horsevents | [horsevents.co.uk](https://horsevents.co.uk) |
| Horse Monkey | [horsemonkey.com](https://horsemonkey.com) |
| My Riding Life | [myridinglife.com](https://myridinglife.com) |
| Riding Diary | [ridingdiary.co.uk](https://www.ridingdiary.co.uk) |
| Equipe | [entry.equipe.com](https://entry.equipe.com) |
| Cotswold Cup | [cotswoldcup.co.uk](https://cotswoldcup.co.uk) |
| Blackwater Farm | [blackwaterfarm.co.uk](https://blackwaterfarm.co.uk) |

---

## 🏗️ Architecture

Nightly **Azure Function** (timer) scrapes all sites over **HTTP**, parses **HTML/JSON**, writes normalized data to **Azure Blob Storage** as **JSON**. **Blazor WebAssembly SPA** loads that JSON once via **HTTP GET**; all filtering and search run in the browser.

![UK Horse Event Data Aggregation Architecture](uk-horse-event-architecture.png)

Flow: *9 sites → Azure Functions (multithreaded, ~3 min) → Blob Storage (JSON) → Blazor SPA → user (data loaded once).*

- **Frontend:** Blazor WebAssembly (.NET 10), static hosting, Bootstrap, infinite scroll, favorites (localStorage), persistent filter preferences (localStorage).
- **Backend:** Azure Functions (daily ~5 AM UTC), C# .NET 10, Blob Storage. Geocoding: Google Geocoding API, Postcodes.io.
- **Tests:** NUnit, unit tests for scraping and domain logic.

---

## ✨ Features

- **Aggregation:** 9 sites, concurrent scrape, fallback to last good data on failure, deduplication, multiple date-format handling.
- **Search & filter:** By date, location, text; by distance from UK postcode (radius in miles); results sort by distance when postcode set.
- **Geospatial:** Postcode validation, Haversine distance, geocoding of venues.
- **UX:** Favorites, infinite scroll, responsive, client-side filtering (instant), persistent filter preferences.

---

## 📁 Project structure

- **Blazor app** – frontend (Pages, Services, wwwroot).
- **Scraper Functions** – timer-triggered Azure Function that runs the pipeline.
- **Scraper library** – base scraper + one scraper per site; runner; Azure Blob helpers.
- **Domain library** – event/location models, locations manager, search-optimised dataset.
- **Test projects** – scraper and domain unit tests.

---

## 🔮 Future enhancements

- Browser geolocation (with consent)
- More event sources
- Calendar export

---

## 📊 Tech & tools

**Stack:** C# (.NET 10), Blazor WebAssembly, Azure Functions, Azure Web App, Azure Blob Storage.  
**Libraries:** ASP.NET Core WebAssembly, Azure.Storage.Blobs, NUnit, Coverlet.  
**APIs:** Google Geocoding, Postcodes.io.

---

*Portfolio project · 2026*
