Step-by-Step Commands Using a User Principal
The Google Sheet file must be owned by or shared with the same User you use to log into Google Cloud.
The User must have a minimum role of Viewer on the Google Sheet file.
The User must have the following roles in the Google Cloud project:
BigQuery User
BigQuery Data Viewer
BigQuery Job User
1. Authenticate
   gcloud auth application-default login
2. Authenticate and enable Google Drive access
   gcloud auth login --enable-gdrive-access --update-adc
3. Test the query
   bq query --use_legacy_sql=false 'SELECT * FROM [GOOGLE_SHEET_TBL]'
   Replace GOOGLE_SHEET_TBL with your actual dataset and table name.

Step-by-Step Commands Using a Service Account Principal
The Google Sheet file must be owned by or shared with the same Service Account in Google Cloud.
The Service Account must have a minimum role of Viewer on the Google Sheet file.
The Service Account must have the following roles in the Google Cloud project:
BigQuery Data Viewer
BigQuery Job User
You will need to download the Service Account private JSON key file.
1. Authenticate
   gcloud auth activate-service-account --key-file=[PATH_TO_YOUR_KEY_FILE]
   Replace PATH_TO_YOUR_KEY_FILE with the path to the private JSON key file.
2. Test the query
   bq query --use_legacy_sql=false 'SELECT * FROM [GOOGLE_SHEET_TBL]'
   Replace GOOGLE_SHEET_TBL with your actual dataset and table name.
