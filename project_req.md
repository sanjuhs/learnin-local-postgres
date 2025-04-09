Introduction - Conf planner part of MIRA ( Market Intelligence Research Agent platform)
Business use case
As I've confirmed with Ishan, the most number of users are 1-5 users for this app concurrently, and it will be majorly used for conference planning (at least this module). We will also use credential-based login (using email and password) for now. Ui will be similar to the prototype currently, with changes given by Ishan as client asks.

From a functionality standpoint, the three parts of the conference planner
pre-conference planner, ( plan the conf for sales people with LLms)
in-conference specialist and ( data parsing layer ⇒ convert everything to text )
post-conference specialist ( convert the text and pics to report )
must be finished.

Standard React libraries with TypeScript. We'll use Shad CN UI for kit bashing and for making the UI for the frontend very quickly. The backend will most likely be using Python, and we'll probably use FastAPI itself as it can be used. We will now lay out an API schema for that over here.
Timeline:
To complete this in a 2 week time period from 7th April.
Monitoring and Observation
Log Rocket for monitoring / post hog for observing what we are doing on front end and backend.

—
Technical Specification

Frontend:
Shadcn UI + React + Vite project hosted on vercel.

Backend:
Python + fastAPI

API spec:

Database Schema Discussion

We will need DB = postgres / RDS for storage
Store the data records that we have from the current excel sheet
JSON B ⇒ extra columns

Your data will come in many, many different columns. Your data can have maybe 15 columns. It can have maybe five columns. It can have N number of columns, but we are then going to map each of the column headers with respect to the row-level data that we have defined in Table 1.
Option 1:
Basically we are using an LLM to read all the headers that are already present inside the data. Then that LLM will match that data with the row-level data in Table One.

Let's assume you have an input Excel ⇒ We will write code to first read the first row of the first sheet which will be the column headers, ⇒ We then pipe these column headers (basically we copy all of these column headers, put them in a string, and send it to an LLM) and also give the column headers for the row-level data in Table One ⇒ We then ask the LLM to match which one matches with what in a JSON ⇒ Take this matched data and then insert it inside the row-level data.
Other option 2:
Assume that the scraped data already comes in a legible format as given in the row-level data of Table 1. In the scraping step itself, we make sure that the data is as per the data in Table 1. That way you can just do a direct insert.

Table 1
Row level Data
Scraped-Data-id = 0001 //string
Stage // enum “scraped-data” ,”processed-data”
Full Date, // string
Day, // string
Date,Time (CEST), // date and time format with UTC
Session Time, // string
Session Title // string
Room // string
Presentation Title // string
Presenter // string
Abstract // string
// other columns to be stored in JSONB format ⇒ aditiondata stored as JSON in JSONB
{
“Presentation URL”: “https://cattendee.abstractsonline.com/meeting/20620/presentation/3087”

}

Table 2
Data table for upload data
Scraped-Data-id = 0001 //string
S3 URL //string
Uploaded time/ date //string
Stage: // enum
Parent-id: //string
Metadata : //JSONB

Table 3
Prompt table:
Prompt -id // string
Prompt
Tags // string
MetaData: JSONB

Table 4 Schedule Table
interface ScheduledEvent {
fullDate: string;
startTime: Date;
endTime: Date;
sessionTitle: string;
room: string;
presentationTitle: string;
presenter: string;
analysisPriorityLevel: string;
isConflicting: boolean;
}

Example data

Full Date
Day
Date
Time (CEST)
Session Time

Session Type.1
Session Title
Room
Presentation Title
Presenter
Presentation URL
Abstract
Monday, September 9, 2024 at 9:00 AM CEST
Monday
2024-09-09 00:00:00
09:00:00
9:00 AM-10:30 AM

Satellite Symposium
PCDE Symposium: Updates from Primary Care Diabetes Europe Research Group
Retiro Hall
Chair
P. Topsever
https://cattendee.abstractsonline.com/meeting/20620/presentation/3087
None

Upload Storage to S3 as a backup

Features:
Scraping of Conference websites in a given format ( of the excel sheet similar to EASD_input automation sheet )
playwri
