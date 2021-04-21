# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.


## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file.
2. Csv file read access support.
3. Email notification dependency, Users information fetch( Email ID's) configeration feature shall be enabled before Tests.
4. File conversion libraries integration.
5. Continous data analysis and data logging plugin like jenkins etc..

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | The Off-the-shelf PDF converter can be indluded by including corresponding library or abstractions.
Counting the breaches       | Yes           | This is one of the requirement, so has to be implemented tested and report shall be delivered
Detecting trends            | Yes           | This is one of the requirement, so has to be implemented tested and report shall be delivered
Notification utility        | Yes           | Failure notification is one of the important feature and shall be implemented and tested to add value to entire implementation and to              take effective actions when such notification is delivered

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. To test if email triggering is working fine.
4. To Test if system timing and logging is according to expecations.
5. To check if the report generation is successfull.
6. False positive check done to see when server is inaccessible how the system behaves. Give a non working server as input to testcase and check the behaviour in this case.
7. Breach information tests when not within limits.
8. Make the system fail by introducing false breaches to the system to check the software.
9. When the report is generated valid stake holders are notified timely-> Testcase to see post report generation the delivrables are delivered correctly.
10. Acceptance tests for positive usecases of the requirement. behaviour during no breaches shall be verified.
11. Test during missing inputs. -> Write a testcase to inform users regarding missing inputs like email ID or sensors not workinge etc.
12. Pre-Requisitis testing check testcase. FOr the feature to run mandatory pre-requisitis check, like data loggers etc shall be checked and if not present users shall be informed with test reports if not present.
13. Regressive testcase(Stress Tests). Calculate the behavrious by running function cyclically for every 30mins for all usecases.
14. Static Tests from Ranging from Experience review to Walkthrough review to come up with past failure and creation of tests for the same.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | report notification via Email|mock the notifier function
Report inaccessible server | server error reading | report server connection problem               | fake the inaccessible server handling function
Find minimum and maximum   | csv file  | comparision between mininum maximum and expected value               | None - it's a pure function
Detect trend               | csv file  | output trend measured with timestamp             | None - it's a pure function
Write to PDF               | html logs, .rtf( Rich Text format), csf conversion  | All deliverable artifacts of "Trend analysis" and "minimum and maximum logged per time stamp" | fake the Pdf converter 
