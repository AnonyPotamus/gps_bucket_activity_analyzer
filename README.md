GCS Bucket Activity Analyzer (gcs-bucket.py)

This script identifies Google Cloud Storage (GCS) buckets that haven't been modified since a specified date. It's useful for identifying unused or stale storage resources that might be candidates for cleanup or archival.
Features:

Scans all buckets in a specified GCP project
Checks bucket metadata and object modification dates
Outputs results to an Excel file for easy analysis
Uses parallel processing for faster execution
Comprehensive logging

Prerequisites

Python 3.6 or later
Google Cloud SDK installed and configured
Required Python packages:
google-cloud-storage
openpyxl => pip install google-cloud-storage openpyxl

Installation

Clone this repository:
bashgit clone <repository-url>
cd gcp-scripts

Install the required packages:
bashpip install -r requirements.txt

Set up authentication:
bashgcloud auth application-default login

Usage
python3 gcs-bucket.py <gcp project id> <start date yyyy-mm-dd> --output <outputfilename>.xlsx --max_workers 10

Arguments:

gcp project id: Your GCP project ID
start date yyyy-mm-dd: Date in YYYY-MM-DD format to check against (buckets not modified since this date will be reported)
--output: (Optional) Output Excel file name (default: unmodified_buckets.xlsx)
--max_workers: (Optional) Maximum number of worker threads (default: 10)

Example:
python3 gcs-bucket.py my-gcp-project 2023-01-01 --output stale_buckets.xlsx --max_workers 10

This command will find all buckets in the project "my-gcp-project" that haven't been modified since January 1, 2023, and save the results to "stale_buckets.xlsx" using 20 worker threads.
Output:
The script generates an Excel file with the following information for each unmodified bucket:

Bucket Name
Created Date
Last Modified Date
Location
Storage Class


Permissions Needed
The service account or user running the script needs the following permissions:

storage.buckets.list
storage.buckets.get
storage.objects.list


