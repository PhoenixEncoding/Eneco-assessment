Eneco BTO Data CODE assessment
---
Date: 2022-02-10

The following exercises are designed to be a quick assessment of candidates affinity with handling data and general-purpose software/scripting tooling.

It is expected that you will spend a maximum of 2 hours working on these exercises. It is OK if you do not complete all exercises in this time. It is up to you on which exercises you spend your time. The exercises can be completed in any order. The choice of tooling to conclude any of the exercises is up to the candidate. Some pointers that might influence your choices;
- Favor fast/pragmatic results over rigid engineering
- How is your solution impacted by any form of automation?
- What is the "resistance to change" of your solution? (e.g; new requirements, other insights, etc..)

You are requested to provide a summary write-up of your results. If you have any code to share, please include that as well. Note that some assignments are intentionally vague. You're free to make any assumptions you think are necessary, but be prepared to defend the choices you made.

Consider the following 3 datasets. These are all used in some way in subsequent exercises;
  - [airports.csv](https://sacodeassessment.blob.core.windows.net/public/airports.csv)
  - [countries.csv](https://sacodeassessment.blob.core.windows.net/public/countries.csv)
  - [runways.csv](https://sacodeassessment.blob.core.windows.net/public/runways.csv)


## 1. Acquire this data and make it suitable for insights

One of your colleagues from the business development department is analyzing a possible market fit for an innovative new product idea. He'd like to derive some insights from the supplied datasets.

Answer, or provide the means to answer, the following questions;
  - Which are the top 10 countries by number of airports (with counts)?
  - Which are the bottom 10 countries by number of airports (with counts)?
  - For every country that has an airpoirt, list the width and length of the longest runway (and name of the airpoirt with that runway).

## 2. Upload airports dataset to "Cloud Storage"

For loading the data into our state-of-the-art Data Warehouse, the data should be supplied, well-formatted, in a block-storage service.

We request a dataset containing at least the columns one of the resultsets from (1) to be supplied to an Azure Blob Storage service (details below, format of choice). If you have no result sets, use some attributes of choice from the [airports.csv](https://sacodeassessment.blob.core.windows.net/public/airports.csv) set.

Details;
```
Azure Storage Account Name            : sacodeassessment
Azure Storage Account Shared Signature: se=2022-03-10T15%3A46Z&sp=rcwd&spr=https&sv=2018-11-09&sr=c&sig=Wf6AQ%2BoLm3mtRq%2BHTvvGt7BzBmUOqz/4QPzTUezcUZo%3D
Blob Storage Container                : results
Target blob path                      : /ingest-airports-{date:yyyyMMdd}-{yourname}
```

## 3. Acquire data from vendor API

Our supplier of high quality, curated country data no longer provides access to a file-based dataset (csv). Instead, they request you the gather this data through their next-generation data broker platform, in exchange for a detailed overview of revenues generated from this data.

Gather country data for every country listed in the airfields dataset and store this in a single file. Next, upload an empty file named 'revenues.txt' to the upload endpoint (HTTP POST).

Which countries information is missing from the broker platform?

Details;
```
client id                   : abc123
host address                : code-assessment-001.westeurope.cloudapp.azure.com:80
HTTP path (get country info): /countries/{iso_code}
HTTP path (upload data)     : /revenues?client={client_id}
```

## 4. Halt excessive API usage

One of your colleagues, Bob, made an automatic collection script to retrieve data from a world-leading SaaS solution. However, the API usage is billed per call and expenses run rampant. The script needs to be stopped ASAP. Fortunately for Bob, but unfortunately for you, Bob is enjoying his holiday. All you know is that Bob's script runs somewhere on a server as a cron job.

Stop Bob's script! Although even better would be to just limit the frequence of his script to execute once every hour during office hours.

Also, find and retrieve the picture of Bob's cats.

Details;
```
server address   : 13.80.255.97
ssh port         : 22
user             : bob
password (of Bob): bob12345@bob
```

## 5. Navigate eCommerce RDBMS

As we're diversifying into digital media, an eCommerce ERP system (Chinook) has been build to handle all inventory tracking and sales for this new retail market.

Larry, a colleague marketeer, pitches an idea involving machine learning based customer segmentation for targeted advertising. He assumes more revenue can be generated from 'more sophisticated' customer - those who enjoy jazz music.

Prove, or disprove, Larry's hypothesis by showing the average of the total value of all sales for a customer who has purchased any jazz music track versus the average value of all sales for customers who have never bought any jazz. Use Larry's credentials to access the chinook system.

Also, Larry confides in you and reveals his next killer-app prototype. It's an app where users can enter any track name and all albums that include that track are listed in the app. Unfortunately Larry is struggling with the performance of a query he needs to run. Can you give Larry or the database administrators a suggestion beneficial to this use case?

```sql
SELECT album.title
FROM   track
JOIN   album ON (track.album_id = album.album_id)
WHERE  LOWER(track.name) = LOWER('Enter Sandman')
```

Details;
```
PostgreSQL Server v13
hostname: code-assessment-001.westeurope.cloudapp.azure.com
port    : 5432
database: chinook
username: larry
password: Ken send me
note    : when to many failed connection attemps are made, your client IP address will be blocked for 1 hour!
```

## 6. HTTP service integration

You receive an email from a colleague, who is developing a software product that uses the HTTP api you helped building and which was release last week.

```
From: bob@eneco.com
Date: Tue Mar 23 10:21:58 AM CET 2021
Title: Your API is broken!

Hi!

I just tried to invoke your API, but I'm only receiving 'Unauthorized' responses. I executed the call exectly as you showed me when you demonstrated the API's usage yesterday.

What's going wrong? Did you fill the server disks completely with funny cat pictures again?

Gr, Bob
```

You take a look at the access log of your server and notice a lot of 401 responses where the following token is used: `eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyIsImtpZCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyJ9.eyJhdWQiOiJodHRwczovL0VuZWNvLm9ubWljcm9zb2Z0LmNvbS9lY3Nhei1hcGlnZWUtb2RwLXQiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9lY2EzNjA1NC00OWE5LTQ3MzEtYTQyZi04NDAwNjcwZmMwMjIvIiwiaWF0IjoxNjE2NDE2NzA1LCJuYmYiOjE2MTY0MTY3MDUsImV4cCI6MTYxNjQyMDYwNSwiYWlvIjoiRTJaZ1lFZzNWZG1mNmhzcHYvdVBNYmZmOC9NQ0FBPT0iLCJhcHBpZCI6IjFlMGZiMzU0LWE3OGQtNGY1Yi05OTY2LWVkNjIzYTYyNDU5OSIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0L2VjYTM2MDU0LTQ5YTktNDczMS1hNDJmLTg0MDA2NzBmYzAyMi8iLCJvaWQiOiJkYjZlODlmOS1kYjE2LTQyNTItOTQyOS1jNGQ1ZTQ4YWRhYmQiLCJyaCI6IjAuQVFVQVZHQ2o3S2xKTVVla0w0UUFad19BSWxTekR4Nk5wMXRQbVdidFlqcGlSWmtGQUFBLiIsInJvbGVzIjpbIlJlYWRXb29uRW5lcmdpZSIsIlJlYWRFbmVjbyIsIlJlYWRPeHhpbyIsIlJlYWRFbmVjb0J1c2luZXNzIiwiUmVhZEFsbCJdLCJzdWIiOiJkYjZlODlmOS1kYjE2LTQyNTItOTQyOS1jNGQ1ZTQ4YWRhYmQiLCJ0aWQiOiJlY2EzNjA1NC00OWE5LTQ3MzEtYTQyZi04NDAwNjcwZmMwMjIiLCJ1dGkiOiJTZ0JhN1EzS1RVeTNRZjhoek9ZM0FBIiwidmVyIjoiMS4wIn0.AZRHBIxtI9uOT99Q0WRII1wPLKbrcBU-BHmQfUvaCCAnKApOZyrH3kxxtYjejgDTnoPIS0I1NnH0pxNd2ATN_50fcHjsXkCr3DaspJggLS_p2rT2nBMkTDyPBKIzw6rZ9tRrwsuFVXh2cYP1kIgoX-_PxpWfzIsyXctcSzbgYnLOJpiVDiZuz_hi4YWbmvc_lO5iezLLpXvQ0ER034tco9An6LtAGH0mK0-4FHW4McQGLpWPXhwAVLRzNdCXx4TNnOK7eDAVyvxf_fD_lbG9OSmd-PnLbFJKHwWNan06D7hTC8yQa4k-k0gcnHjDYKirG7CfnR5b6dKSst-BCa3X9w`. There are no observed layer 4 anomalies.

What could this token represent and how is it typically used? Can you derive some details from this token? Describe the steps you would take to further analyze Bob's issue before you will respond to his email.
