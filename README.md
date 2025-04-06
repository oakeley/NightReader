# NightReader - Insulin Data Analysis Tool

A comprehensive tool for fetching, analyzing, and visualizing insulin usage data from Nightscout deployments.

## Overview

NightReader is a Python-based utility that helps people with diabetes analyze their insulin usage patterns over time. It connects to a Nightscout deployment, retrieves insulin data, and generates insightful visualizations including:

- Daily insulin consumption breakdown (bolus vs basal)
- Insulin usage trends over time
- Monthly median insulin usage analysis

The tool also supports caching data locally to avoid repeated API calls, and can export data in multiple formats for further analysis.

## Features

- **Complete Data Retrieval**: Fetches all insulin records using pagination, ensuring no data is missed
- **Smart Caching**: Saves downloaded data to avoid redundant API calls
- **Comprehensive Analysis**: Calculates daily, monthly, and overall statistics
- **Multiple Export Formats**: Supports CSV, TSV, Excel, and JSON exports
- **Rich Visualizations**: Creates detailed graphs of insulin usage patterns
- **Monthly Analysis**: Provides monthly median insights for tracking long-term patterns

## Installation

### Prerequisites

- Python 3.8 or higher
- A running Nightscout deployment

### Setup with Conda

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/nightreader.git
   cd nightreader
   ```

2. Create and activate the conda environment:
   ```bash
   conda env create -f xdrip_env.yml
   conda activate xdrip_analysis
   ```

### Setup with pip

If you're not using conda, you can install the required packages with pip:

```bash
pip install pandas matplotlib requests numpy
```

## Usage

### Basic Usage

```bash
python nightreader.py --url https://your-nightscout-site.com --start-date 2024-01-01 --end-date 2024-12-31
```

### Command Line Options

| Option | Description |
|--------|-------------|
| `--url` | Your Nightscout URL (e.g., https://your-nightscout-site.com) |
| `--start-date` | Start date in YYYY-MM-DD format |
| `--end-date` | End date in YYYY-MM-DD format |
| `--api-key` | Nightscout API key/token if required |
| `--output` | Output file path for the plot (e.g., insulin_report.png) |
| `--debug` | Enable debug mode for verbose output |
| `--export-csv` | Base filename for exporting data |
| `--export-formats` | Comma-separated list of formats to export (csv,tsv,xlsx,json) |
| `--import-csv` | Import data from a previously saved CSV file |
| `--no-trend` | Disable trend line in plot |
| `--no-monthly` | Disable monthly median plot |
| `--data-dir` | Directory to store/retrieve cached data (default: ./data) |
| `--force-refresh` | Force refresh data from Nightscout even if cached data exists |

### Example Workflows

#### First-time analysis of a year of data

```bash
python nightreader.py --url https://your-nightscout-site.com --start-date 2024-01-01 --end-date 2024-12-31 --debug --output insulin_2024.png
```

#### Analyze data with automatic caching

```bash
python nightreader.py --url https://your-nightscout-site.com --start-date 2024-01-01 --end-date 2024-12-31 --data-dir ./insulin_data
```

#### Export data to multiple formats

```bash
python nightreader.py --url https://your-nightscout-site.com --start-date 2024-01-01 --end-date 2024-12-31 --export-csv insulin_data_2024 --export-formats csv,tsv,xlsx
```

#### Use previously saved data

```bash
python nightreader.py --import-csv insulin_data_2024.csv --output insulin_report_2024.png
```

## Interpreting the Results

### Daily Insulin Chart

The tool generates a two-part chart:

1. **Top Panel**: Stacked bar chart showing:
   - Daily bolus insulin (usually mealtime, in dark blue)
   - Daily basal insulin (if available, in light blue)
   - A red dotted line showing the daily average

2. **Bottom Panel**: Line chart showing:
   - Total daily insulin with trend analysis
   - The slope of the trend line indicates whether insulin usage is increasing, decreasing, or stable over time

### Monthly Median Chart

A separate chart shows:
- Monthly median insulin usage (only for months with at least 3 days of data)
- Bolus vs basal breakdown for each month
- The number of days with data for each month
- A red dotted line showing the overall median

### Statistics Output

The tool also prints detailed statistics to the console:
- Total days in the date range
- Days with insulin data and coverage percentage
- Daily average insulin (total, bolus, and basal)
- Total insulin used in the period
- Monthly median statistics for each month

## Data Privacy and Security

All data is processed locally on your machine. The tool only connects to your Nightscout instance to retrieve data and does not share or upload any information elsewhere.

## Troubleshooting

### Missing Data

If you're seeing fewer days of data than expected:
- Enable `--debug` to see detailed API responses
- Check if your Nightscout instance has data retention limits
- Try using smaller date ranges if fetching a large period

### API Errors

If you encounter errors connecting to Nightscout:
- Verify your Nightscout URL is correct and accessible
- Check if your instance requires an API key
- Ensure your Nightscout version is compatible

## License

This project is licensed under the GNU v3 License - see the LICENSE file for details.

## Acknowledgments

- The Nightscout community for their amazing work on diabetes data visualization
- All contributors to this project

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
