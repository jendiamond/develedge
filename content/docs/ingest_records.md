---
title: "Ingest Records Locally - Californica"
date: 2019-05-19T21:29:48-07:00
draft: true
---

### Ingest Records Locally

1. Go to https://github.com/UCLALibrary/eureka and download the csv files you want to use.
    + Bennet has 79 records  
    + Connell has 502 records
    + LA Daily News has over 5000
    + The ingest time is about 5 seconds per record
1. Go to the californica local host http://localhost:3000/
1. Sign in Email: admin@example.com Password: password
1. Once you sign in click "Import Contenr From a CSV" in the sidebar
1. This opens the page that reads "Import a set of records
1. Click "Upload your CSV"
1. Where it says "Type a directory path" type in the letter x
    + Type a directory path where your binary attachments can be found. It should look something like this: /opt/data/Masters/dlmasters/bennett/masters.  Note that only directories inside /opt/data will work.
1. Click the "Preview Import" button
1. Then you will be on the page "Preview of your CSV-based Import" Click the "Start Import" button
1. Your items are now importing

