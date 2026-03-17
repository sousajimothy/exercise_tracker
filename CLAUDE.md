# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Purpose**: A system for tracking and performing advanced analytics on exercise data. Primary data source is screenshots from fitness watch apps (e.g., Garmin, Apple Watch, Fitbit). Future enhancement will include API integrations for automated data extraction.

**Key Features**:
- Screenshot ingestion and parsing
- Exercise data extraction and normalization
- Advanced analytics and trend analysis
- Multi-source fitness watch support

## Development Setup

### Prerequisites
- Python 3.9+ (primary language for data processing and analytics)
- Dependencies managed via `pip` and `requirements.txt`

### Common Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run tests
pytest

# Run specific test file or test function
pytest tests/test_specific.py
pytest tests/test_file.py::test_function_name

# Lint code
flake8 src/ tests/

# Format code (if using black)
black src/ tests/

# Run the application
python -m exercise_tracker.main
```

## Architecture Overview

The project is organized into logical domains:

1. **Data Ingestion** (`src/ingestion/`)
   - Screenshot handling and upload
   - Image preprocessing and validation
   - Multi-format fitness watch app support

2. **Data Extraction** (`src/extraction/`)
   - OCR and text extraction from screenshots
   - Structured data parsing (extracting metrics like distance, duration, calories)
   - Watch app-specific parsers (Garmin, Apple Watch, etc.)

3. **Data Normalization** (`src/normalization/`)
   - Standardizing data across different watch formats
   - Handling missing or invalid data
   - Creating a unified exercise data model

4. **Analytics** (`src/analytics/`)
   - Trend analysis
   - Performance metrics and summaries
   - Statistical insights

5. **API Layer** (`src/api/`)
   - REST endpoints for uploading screenshots
   - Analytics query endpoints
   - Future fitness watch API integrations

6. **Database** (`src/database/`)
   - Exercise record storage
   - User data persistence
   - Query interface

## Key Patterns and Decisions

### Data Model
- Exercise records store: activity type, duration, distance, calories, date/time, heart rate metrics, source watch type
- Records are immutable after creation; corrections create new records with references to originals
- All timestamps use UTC internally; converted to user timezone on display

### Screenshot Processing Pipeline
- Input → Validation → OCR/Extraction → Parsing → Normalization → Storage → Analytics
- Each step has error handling and logging for debugging
- Screenshots are archived after successful extraction

### Testing
- Unit tests for extraction logic and data normalization (test with known screenshots)
- Integration tests for the full pipeline
- Tests include fixtures for different watch formats

## Future Enhancements

When implementing API integrations with fitness watches:
- Abstract the data extraction layer to support both screenshots and API responses
- Maintain backward compatibility with screenshot-based workflows
- Add authentication/credential management for API keys
