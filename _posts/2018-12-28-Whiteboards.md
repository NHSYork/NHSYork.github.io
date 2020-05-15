---
layout: post
published: true
title: Electronic Whiteboards using Oracle APEX
tags: [OrclApex,Showcase]
bigimg: /img/cropped-aPicture8.jpg
---

## Electronic Whiteboards

We have used [Oracle APEX](https://apex.oracle.com/) to create different display "boards" that support the care of Patients during their stay in our hospitals. These boards have been developed in-house by our own developers over a number of years. They are built directly on the Oracle database that is used for our Patient Administration System.
Located throughout the hospitals at the point of use, most of these boards are permenantly "on" and require no user input. They auto-refresh to update every few minutes to reflect changes made on the patient administration and clinical systems. Some allow users to authenticate by entering their normal system credentials and drill down to see more information or update the patient record.
These systems are designed to support the specific care of individual patients and the management of the flow of patients through the hospitals.

### Emergency Department Boards

There is a display board that shows all patient within the Emergency Department (ED). This can be launched with a location parameter to show a shorter list of patients to those staff in that area, whereas others will show full lists of ED patients.
So for example here we can see the patients waiting in the Ambulance arrivals area.

![EDAmbulance.jpg](/img/EDAmbulance.jpg)

The board shows:
- The cubicle in which the patient is located
- The patient's initials, sex and age
- Visual indicators. Here we can see the forget-me-not which indicates dementia, a ceiling of care alert and frailty flags
- The most recent National Early Warning Score (NEWS) and the time since the observations were taken
- Whether the patient has been streamed or assessed and the priority level
- Whether or not the patient has been seen by a doctor, by whom and at what time
- The responsible consultant
- If a treatment decision has been reached and how long has elapsed since the patient has been seen by a doctor 
- If canulae have been fitted
- If there are pathology or radiology results to view
- Key tasks the patient is waiting for (and for how long)
- The Glasgow Admission Prediction Score
- If the patient is ready for transfer
- For patients flagged for admissison the destination is shown (once recorded)
- If the ED Coding has been completed
- Total time in ED and the projected breach time

Most of the data items have pop up tooltips or the users can drill downs to see more detail. All the data is held in the main ED/PAS system and queried directly. Users can authenticate using their normal network logon and perform limited updates - for example recording times, creating or acknowledging tasks.

### Arrivals Boards

The Arrivals Boards are loacted within the admitting ward areas and the control room as "permenantly on" displays. They show patients that are on their way to the wards as well as patients already admitted onto a ward. They clearly show the status of a patient in relation to their being seen by an admitting doctor. This is a key safety factor in ensuring patients get seen quickly and don't get missed.

![arrivalsbd.png](/img/arrivalsbd.png)

The screens can be configured to show specific specialties, groups of specialties or all patients. 

The board shows:
- The location of the patient (or their intended location if they are still in ED, or coming directly from Primary Care)
- LoS (legth of Stay)
- Reason for admission & who discussed the admission 
- Sepsis Screening Status
- Clerking Status (TBS = To Be Seen)
- A flag to show if the patient can outlie (i.e. be sent to a ward belonging to a different specialty)
- RFT - is the patient ready to transfer?

### Activity Predictor

We stream data to an Oracle 11gR2 database using Oracle Streams. We have a transformation process which runs every 15 minutes that updates the "real time" data that is displayed in this screen. This shows the position in relation to attendances to the Emergency Department and admissions and discharges within the two acute hospitals.
Current statistics are shown alongside averaages, upper and lower control limits based on activity data over the preceeding two years. Colour coding is used to give a quick indication of the state of the hospital.

![edactivitybd.png](/img/edactivitybd.png)

### Bed Status
This board shows the bed stock of the Hospitals (only one shown in the screenshot below)
Bed managers can see the location of available beds, if they are male or female and the numbers of expected discharges today and tomorrow.

![bedstock.JPG](/img/bedstock.jpg)

Clicking the ward shorname/number will drill down into the Ward Whiteboard so they can review the detailed position on each ward.
The screen auto-refreshes every ten minutes, but can be manually refreshed.

### Ward Whiteboard
These screens were not written in Oracle APEX, but were created using java server pages and oracle reports server. It's not how we would do them today, but they have been robust and stood the test of time.
There are one or two of these screens on each ward, they are set up on PCs that are always on and auto-start directly to the whiteboard screen.

![origwhiteboard.png](/img/origwhiteboard.png)

The screen shows an approximate layout of the ward and clearly identifies the occupied beds as well as patients who have arrived but have not yet been allocated to a bed. The screenshot above is from our test database and is from a presentation we did in 2007. The screens were first put live in 2006 and are still in use. You can see the patient, which consultant is responsible for their care, which nursing team and some clinical information such as their NEWS, diabetes flags etc.
On the current version you can drill down to see their nursing observations chart.

### Patient Board

The Patient Board is the main working list for a Ward within the hospital. It is used to highlight the current status of a patient in relation to health indicators and activity. 

![PatientBoard.JPG](/img/PatientBoard.jpg)

As with the ED Board there are indicators for Patients with Diabetes, Frailty, Dementia, Ceiling of Care etc. The board also shows the following which are pulled directly from the electronic patient record:

- Blood Glucose Levels
- Nutrition Score
- Waterlow Score (Skin assessment)
- Falls Assessment
- Number of Canulae (if fitted)
- Clerking Status
- Indicator if any Pathology has been reported, showing as a red cross until it is reviewed
- Similar indicator for Radiology
- VTE assessment Status
- Allergy Review Status
- AMTS Status
- Diagnosis Status
- Discharge Drug (TTO) indicator
- Flag showing if the electronic discharge letter has been done (for patients approaching transfer)
- Discharge status indicator
- Flag showing if the patient can outlie

The board is instrumental in supporting discharge planning. You can see what the patient is waiting for, the details of any delays and where the patient will be discharged to. The screen shows details of any internal referrals and interactions with Social Services for Delayed Transfers of Care.
During a "board round" or huddle, a user can log in using their normal Single Sign on and perform updates.


### Transfers Board

![Transfers.JPG](/img/Transfers.JPG)

This screen gives an overview of the whole hospital or specialty, showing a patients current location along with their intended destination location. It includes patients in the Emergency Department and patients who are being admitted directly from their GP. The board indicates when the patient is ready for transfer and how long they have been waiting. It also highlights available beds though the hospital.

### Departures

![departures.JPG](/img/departures.JPG)

The departures board is more interactive than most of our other electronic bards, having a number of parameters allow users to search for patients meeting specific criteria.

#### Some Site Photos 

![EDphoto.JPG](/img/EDphoto.JPG)
Nursing Station in Emergency Department Showing the ED Board on the large screen.

![bedoffc.jpg ](/img/bedoffc.jpg)
A wall of the Operations Control Centre showing large screens configured to show Patient Boards for the entire hospital.

![IMG-20170521-WA0000.jpg](/img/IMG-20170521-WA0000.jpg)
Another view showing boards. 
The Dark blue screen is the Ambulance System - showing patients on their way to ED. This is not our system, but is supplied by the Yorkshire Ambulance Service.

 





