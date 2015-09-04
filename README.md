onebusaway-watchdog
===================

onebusaway-watchdog is a Python-based watchdog application for your [OneBusAway (OBA)](http://onebusaway.org/) REST API server that 
occasionally checks API responses for valid real-time transit data.  It keeps an eye on your OBA server
so you don't have to.

onebusaway-watchdog performs the following tasks:

1.  Tests for the success of various API queries on OBA.
2.  Tests that there is realtime data available for >50% of buses currently running.
3.  Tests that unrealistic results (e.g.,100% ontime performance) aren't being returned

If an issue is detected, an email is generated with an Alert # and a description of the problem.
The watchdog will then stop running until that Alert is addressed (to prevent emails would keep piling up).
When someone replies back to the email, the Alert is closed and the watchdog resumes.

### Setup
Since onebusaway-watchdog generates email alerts, it requires the email addresses of the people
to contact when there are problems, as well as the credentials for an email server.  Currently,
this information is hard-coded in the script, so you'll need to edit this to meet your needs.

Similarly, the script requires a OneBusAway REST API server address.  This also currently needs
to be edited manually.

You'll also need a [Python interpreter](http://www.python.org/getit/) to run the script.

In this fork, you'll need to put all of the sensitive information in the config file (don't commit passwords!).  Then, just change the '/path/to/watchdog.ini' line in `check_oba.py`.  Listed below are all configuration variables:

| Setting Name | Description |
| --- | --- |
| alert_list | A comma seperated list of emails that will be sent alert emails. |
| api_key | The OneBusAway API key to use. |
| csv_status_file | Path to a file that can be created by the program. |
| days_of_week_to_report | A comma seperated list of 1s or 0s to indicate whether the watchdog script should perform on this day of week.  1=yes. List seven values. |
| end_of_day | The seconds after midnight which checks should not be performed. |
| from_address | The from email that alerts get sent from.  Typically a Gmail address is a good one to use. |
| imap_host | The imap host to use.  If using Gmail, set to `imap.gmail.com`. |
| password | The login password for the email account. |
| realtime_agencies | A comma seperated list of agencies with realtime data. |
| report_hours | A comma seperated list of integers used indicating which hours of the day to send out reports.  Include at least 2 for the script to work properly. |
| report_list | A comma seperated list of emails that will be sent report emails. |
| report_status_file | Path to a file that can be created by the program. |
| root_url | The root URL for the onebusaway-api-webapp. |
| SMTP_HOST | The smtp host to use.  If using Gmail, set to `smtp.gmail.com:587`. |
| start_of_day | The seconds after midnight which checks should start for the day. |
| stop_test_factor | A divisory factor to determine how many stops to investigate realtime data for.  Example num_stops_to_check = total_num_stops / stop_test_factor. |
| username | The login username of the email account. |

### Usage

At the command-line, execute:

`check_oba.py`
