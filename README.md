# Plan My Ride - Equestrian Events Aggregator

> **Portfolio Project** | A full-stack web application that aggregates and displays unaffiliated equestrian events from multiple UK entry systems in a unified, searchable interface.

**Note:** This is a closed-source portfolio project. The codebase is maintained in Azure DevOps and is showcased here to demonstrate technical capabilities and problem-solving skills.

---

## 🎯 Project Overview

**Plan My Ride** solves a real-world problem: equestrian enthusiasts previously had to visit multiple websites to find unaffiliated events. This application aggregates events from 7+ major UK equestrian event entry systems, providing a single, powerful search interface with advanced filtering capabilities.

### Key Metrics
- **7+ event sources** aggregated into one platform
- **Thousands of events** processed and displayed
- **Client-side filtering** for instant search results
- **Distance-based sorting** using geospatial calculations
- **Azure cloud infrastructure** for scalability and reliability

---

## 🏗️ Architecture & Technical Stack

### Frontend
- **Framework:** Blazor WebAssembly (.NET 8)
- **Architecture:** Client-side only, static hosting
- **Key Features:** 
  - Real-time filtering and search
  - Infinite scroll for performance
  - Favorites system with local storage
  - Responsive design with Bootstrap

### Backend & Data Processing
- **Runtime:** Azure Functions (Timer-triggered, runs daily at 5 AM UTC)
- **Language:** C# (.NET 8) with nullable reference types
- **Storage:** Azure Blob Storage (JSON data files)
- **APIs:** 
  - Google Geocoding API (for location coordinates)
  - Postcodes.io API (for UK postcode lookups)

### Infrastructure
- **Hosting:** Azure Web App (Blazor WASM static hosting)
- **Data Pipeline:** Azure Functions → Azure Blob Storage → Static JSON files
- **Scheduling:** Timer-triggered Azure Functions for automated data collection

### Testing
- **Framework:** NUnit
- **Coverage:** Unit tests for core scraping logic and domain models
- **Test Projects:** 
  - `ScraperClassLibrary.Tests`
  - `UnaffiliatedEquestrianEventsCalendarClassLibraryTests`

---

## ✨ Key Features

### 1. Multi-Source Event Aggregation
- Concurrent web scraping from 7+ equestrian event websites
- Robust error handling with fallback to previous data on scraper failures
- Automatic deduplication and data normalization
- Support for multiple date formats and event structures

### 2. Advanced Filtering & Search
- **Date Filtering:** Filter events by specific dates
- **Location Filtering:** Filter by event venue/location
- **Text Search:** Full-text search across titles, descriptions, and disciplines
- **Distance-Based Filtering:** Filter events within a specified radius (miles) from user's postcode
- **Smart Sorting:** Results sorted by distance when postcode is provided

### 3. Geospatial Features
- UK postcode validation and coordinate lookup
- Haversine formula implementation for accurate distance calculations
- Automatic geocoding of event locations using Google Geocoding API
- Distance display for each event relative to user's location

### 4. User Experience Enhancements
- **Favorites System:** Save events to favorites with persistent local storage
- **Infinite Scroll:** Progressive loading for optimal performance with large datasets
- **Responsive Design:** Mobile-friendly interface
- **Fast Client-Side Filtering:** All filtering performed client-side for instant results
- **Error Resilience:** Graceful handling of API failures and data inconsistencies

### 5. Data Processing & Optimization
- Pre-processed JSON datasets optimized for client-side consumption
- Automatic removal of expired events
- Efficient data structures for fast lookups
- Parallel processing of multiple scrapers for improved performance

---

## 🔧 Technical Highlights

### Scalable Architecture
- **Separation of Concerns:** Modular design with dedicated class libraries
  - `ScraperClassLibrary` - Reusable scraping infrastructure
  - `UnaffiliatedEquestrianEventsCalendarClassLibrary` - Domain models and business logic
  - `UnaffiliatedEquestrianEventsCalendarBlazorApp` - Frontend application
- **Dependency Injection:** Proper DI container usage throughout
- **Interface-Based Design:** Testable abstractions with `ILocationsManager`, `IFavoritesService`

### Concurrent Processing
- **Parallel Web Scraping:** Multiple scrapers run concurrently using `Task.WaitAll()`
- **Async/Await Patterns:** Proper async/await usage throughout for non-blocking operations
- **Cancellation Token Support:** Graceful handling of long-running operations

### Geospatial Calculations
- **Haversine Formula:** Accurate distance calculations between coordinates
- **Coordinate Management:** Efficient storage and lookup of location coordinates
- **Postcode Integration:** UK postcode validation and coordinate resolution

### Performance Optimizations
- **Client-Side Filtering:** All filtering performed in-browser for instant results
- **Infinite Scroll:** Progressive rendering to handle large datasets efficiently
- **Optimized Data Structures:** Dictionary-based lookups for O(1) location access
- **Pre-processed Datasets:** JSON files optimized for fast client-side consumption

### Error Handling & Resilience
- **Exception Handling:** Comprehensive try-catch blocks with logging
- **Fallback Mechanisms:** Previous data used when scrapers fail
- **Data Validation:** Input validation for postcodes, dates, and user inputs
- **Graceful Degradation:** Application continues to function even when some features fail

### Code Quality
- **Nullable Reference Types:** Enabled throughout for better null safety
- **Unit Testing:** NUnit tests for core functionality
- **Code Coverage:** Coverlet integration for test coverage metrics
- **Clean Code Practices:** Well-organized, maintainable codebase

---

## 📁 Project Structure

```
UnaffiliatedEquestrianEventsCalendar/
├── UnaffiliatedEquestrianEventsCalendarBlazorApp/    # Blazor WebAssembly frontend
│   ├── Pages/                                       # Razor pages (Index.razor)
│   ├── Services/                                    # Favorites service, etc.
│   └── wwwroot/                                    # Static assets & JSON data
│
├── ScraperFunctions/                                # Azure Functions project
│   └── ScraperRunnerFunction.cs                    # Timer-triggered function
│
├── ScraperClassLibrary/                            # Scraping infrastructure
│   ├── Scrapers/                                   # Individual scraper implementations
│   │   ├── Scraper.cs                             # Base scraper class
│   │   ├── EqEventsScraper.cs
│   │   ├── HorseEventsScraper.cs
│   │   ├── HorseMonkeyScraper.cs
│   │   ├── MyRidingLife.cs
│   │   ├── RidingDiary.cs
│   │   └── WeighedInScraper.cs
│   ├── ScraperRunner.cs                           # Orchestrates scraping process
│   └── Helpers/                                    # Azure Blob Storage helpers
│
├── UnaffiliatedEquestrianEventsCalendarClassLibrary/  # Domain models & business logic
│   ├── Event.cs                                    # Event domain model
│   ├── Location.cs                                 # Location with coordinates
│   ├── LocationsManager.cs                        # Location management logic
│   └── SearchOptimisedDatasetOfAllEvents.cs        # Optimized dataset structure
│
├── ScraperClassLibrary.Tests/                      # Unit tests for scrapers
└── UnaffiliatedEquestrianEventsCalendarClassLibraryTests/  # Unit tests for domain logic
```

---

## 🎨 Screenshots & Demos

<!-- Screenshots and GIFs will be added here -->
<!-- 
### Main Interface
![Main Interface](screenshots/main-interface.png)
*The main event listing with filters and search capabilities*

### Filtering & Search
![Filtering](screenshots/filtering.gif)
*Demonstrating advanced filtering by date, location, and distance*

### Favorites System
![Favorites](screenshots/favorites.png)
*Saving and managing favorite events*

### Mobile View
![Mobile](screenshots/mobile.png)
*Responsive design on mobile devices*
-->

---

## 🚀 Technical Challenges & Solutions

### Challenge 1: Handling Multiple Date Formats
**Problem:** Different event sources use various date formats (e.g., "1st January 2024", "01/01/2024", "January 1, 2024").

**Solution:** Implemented a robust date parsing system with multiple format support using `DateTime.TryParseExact()` with a comprehensive list of UK date formats, including ordinal suffixes (1st, 2nd, 3rd, etc.).

### Challenge 2: Geocoding and Distance Calculations
**Problem:** Events need to be sorted by distance from user's location, requiring accurate geocoding and distance calculations.

**Solution:** 
- Integrated Google Geocoding API for converting addresses to coordinates
- Implemented Haversine formula for accurate distance calculations
- Used Postcodes.io API for UK postcode coordinate lookup
- Cached coordinates to minimize API calls

### Challenge 3: Ensuring Data Freshness While Handling Failures
**Problem:** Scrapers may fail, but users still need access to recent data.

**Solution:** Implemented a fallback mechanism that preserves data from previous successful runs. If a scraper fails, the system uses the last known good data for that source, ensuring users always have access to recent events.

### Challenge 4: Client-Side Performance with Large Datasets
**Problem:** Filtering thousands of events client-side could cause performance issues.

**Solution:** 
- Pre-processed datasets optimized for client-side consumption
- Implemented infinite scroll to render events progressively
- Used `Task.Run()` to offload filtering from UI thread
- Efficient data structures (dictionaries) for O(1) lookups

### Challenge 5: Concurrent Web Scraping
**Problem:** Scraping multiple websites sequentially would be too slow.

**Solution:** Implemented parallel scraping using `Task.WaitAll()` to run all scrapers concurrently, significantly reducing total execution time while maintaining proper error handling and cancellation support.

---

## 🛠️ Development Practices

### Code Organization
- **Modular Architecture:** Clear separation between scraping, domain logic, and presentation
- **Reusable Components:** Base `Scraper` class with inheritance for specific implementations
- **Interface Abstractions:** `ILocationsManager` and other interfaces for testability

### Testing Strategy
- **Unit Tests:** NUnit tests for core scraping logic and domain models
- **Test Coverage:** Coverlet integration for code coverage metrics
- **Testable Design:** Dependency injection and interface-based design enable easy testing

### Error Handling
- Comprehensive exception handling throughout the application
- Logging for debugging and monitoring
- Graceful degradation when external services fail

### Performance Considerations
- Async/await patterns for non-blocking operations
- Efficient data structures and algorithms
- Client-side optimizations for fast user experience

---

## 🔮 Future Enhancements

Potential improvements and extensions:
- Server-side pre-filtering for very large datasets
- Browser geolocation API integration (with user consent)
- Persistent filter preferences in localStorage
- Application Insights integration for telemetry
- Additional event sources
- Email notifications for favorite events
- Calendar export functionality

---

## 📊 Technologies & Tools

### Languages & Frameworks
- **C#** (.NET 8, .NET 9)
- **Blazor WebAssembly**
- **Azure Functions**

### Cloud Services
- **Azure Web App** (hosting)
- **Azure Functions** (scheduled tasks)
- **Azure Blob Storage** (data storage)

### Libraries & Packages
- **Microsoft.AspNetCore.Components.WebAssembly**
- **Microsoft.NET.Sdk.Functions**
- **Azure.Storage.Blobs**
- **NUnit** (testing)
- **Coverlet** (code coverage)

### APIs
- Google Geocoding API
- Postcodes.io API

---

## 📝 Notes

- This project demonstrates full-stack development capabilities, cloud architecture knowledge, and problem-solving skills
- The application is designed to be scalable, maintainable, and performant
- Security best practices are followed (no sensitive information in code, proper credential management)
- The codebase follows .NET best practices and modern C# patterns

---

## 👤 Author

**Software Engineer** | Portfolio Project

*Demonstrating expertise in:*
- Full-stack .NET development
- Azure cloud services and serverless architecture
- Web scraping and data aggregation
- Geospatial calculations and APIs
- Performance optimization
- Modern software engineering practices

---

*Last Updated: 2025*
