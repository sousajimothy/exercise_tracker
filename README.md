# Exercise Tracker

Advanced analytics system for tracking and analyzing exercise data from fitness watch screenshots.

## Overview

Exercise Tracker extracts, normalizes, and analyzes workout data from fitness watch app screenshots (Garmin, Apple Watch, Fitbit, etc.). The system processes images to extract metrics like distance, duration, calories burned, and heart rate data, then provides insights and trends across your fitness activities.

### Key Features

- **Screenshot-based data entry** — Upload screenshots from your fitness watch app
- **Multi-watch support** — Handles different fitness watch formats (Garmin, Apple Watch, Fitbit, and more)
- **Automatic extraction** — OCR and parsing extracts metrics without manual data entry
- **Data normalization** — Standardizes data across different watch brands into a unified format
- **Advanced analytics** — Generate trends, performance metrics, and fitness insights
- **Future API support** — Planned integration with fitness watch APIs for automated data sync

## Getting Started

### Prerequisites

- Python 3.9 or later
- pip (Python package manager)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd exercise_tracker
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Uploading Exercise Data

```python
from exercise_tracker import ExerciseTracker

tracker = ExerciseTracker()

# Upload a screenshot from your fitness watch
result = tracker.upload_screenshot("path/to/screenshot.png")

# Access the extracted exercise data
exercise = result.exercise
print(f"Activity: {exercise.activity_type}")
print(f"Duration: {exercise.duration}")
print(f"Distance: {exercise.distance} km")
print(f"Calories: {exercise.calories}")
```

### Querying Exercise Data

```python
# Get all exercises for a date range
exercises = tracker.get_exercises(
    start_date="2026-01-01",
    end_date="2026-03-17"
)

# Get analytics and trends
stats = tracker.get_stats(
    start_date="2026-01-01",
    end_date="2026-03-17"
)
print(f"Total distance: {stats.total_distance} km")
print(f"Average heart rate: {stats.avg_heart_rate} bpm")
```

## Development

### Running Tests

```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_extraction.py

# Run specific test function
pytest tests/test_extraction.py::test_garmin_parsing

# Run with coverage
pytest --cov=src
```

### Code Quality

```bash
# Lint code
flake8 src/ tests/

# Format code
black src/ tests/
```

### Project Structure

```
exercise_tracker/
├── src/
│   ├── ingestion/          # Screenshot upload and validation
│   ├── extraction/         # OCR and data extraction from images
│   ├── normalization/      # Data standardization and cleaning
│   ├── analytics/          # Trend analysis and metrics
│   ├── api/                # REST API endpoints
│   ├── database/           # Data persistence layer
│   └── models/             # Data models and schemas
├── tests/                  # Unit and integration tests
├── CLAUDE.md              # Claude Code guidance
└── README.md              # This file
```

## Architecture

The system processes exercise data through a defined pipeline:

1. **Ingestion** — Accept and validate screenshot uploads
2. **Extraction** — Extract text and metrics from images using OCR
3. **Parsing** — Convert extracted data into structured exercise records
4. **Normalization** — Standardize data across different watch formats
5. **Storage** — Persist exercise records in the database
6. **Analytics** — Generate insights and trends from the data

Each step includes error handling and logging to ensure data quality and debuggability.

## Supported Fitness Watches

Currently supported:
- Garmin (Forerunner, Fenix, Epix, etc.)
- Apple Watch
- Fitbit

More watch types can be added by implementing a parser in `src/extraction/parsers/`.

## Future Enhancements

### API Integrations

Planned support for direct API connections to fitness watch platforms, enabling automated data sync without manual screenshots:

- Garmin Connect API
- Apple HealthKit
- Fitbit API
- Strava API

### Analytics Features

- Weekly/monthly performance summaries
- Personal records tracking
- Workout comparison and progression
- Heart rate zone analysis
- Route mapping and visualization

### User Interface

- Web dashboard for viewing exercise history
- Data import/export functionality
- Custom analytics and report generation

## Contributing

Contributions are welcome. Please ensure:
- All tests pass (`pytest`)
- Code is formatted (`black`)
- Code is linted (`flake8`)
- New features include tests

## License

[Add license information]

## Support

For issues, questions, or feature requests, please open an issue on the GitHub repository.
