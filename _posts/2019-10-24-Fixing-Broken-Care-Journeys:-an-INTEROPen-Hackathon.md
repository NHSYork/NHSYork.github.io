_by Anne Jessop_
### [#FHIRHack19](https://twitter.com/hashtag/FHIRHack19)
A team of 3 developers from York Teaching Hospital NHS Foundation Trust attended the Leeds INTEROPen hackathon on 14-15 October 2019.

Our focus for the two days was Medicines Reconciliation. As an Acute Trust, we were most interested in receiving data from GP software and being able to accurately and quickly ensure that all the drugs that the patient is taking are reconciled on our system.

## Patient Safety Benefits
Prescribers would have access to medication related information at all times, which would mean a reduction in:
* Essential drugs not prescribed
* Wrong drugs prescribed
* Wrong doses and frequencies prescribed
* Missed and delayed doses, including critical and time-critical meds
* Transcription errors by prescribers and pharmacy staff

## Time Savings
The number of transcriptions by pharmacy staff would decrease as prescribers would have the admission medication details from the beginning. The time that it takes to transcribe drugs from Summary Care Records (SCR) to our Electronic Prescribing system (EPMA) differs depending on the number of drugs that need transcribing. It would take the average person approximately 15 to 25 secs to enter each drug if a suggested dose exists for it, a little longer if not. Also to add to this, is the time for interpretation of the SCR prior to transcribing.

## Excitingly, over the two days we managed to develop a working solution!
There are still some things to work out for a seamless interaction, but it is definitely a huge step in the right direction.

The largest barrier in medicines reconcilliation between systems is that hospitals use dose based prescribing (e.g. 75mg aspirin in dispersible tablet form) wheras GP and dispensing  systems use product base prescribing (e.g. 1 tablet of 75mg aspirin dispersible tablet).

Things we learned:
* GP Connect standards currently don’t enforce dose and frequency to be coded. As such, the conversion between ‘1 tablet of 75mg strength’ and ‘75mg’ is not possible.
* FHIR standards allow for the dose and frequency to be passed in coded form. We use FDB Multilex drug database and it is possible to convert from one form to the other using their mapping tables so long as the dose and frequency are coded. 
* GP systems do not include medication route (e.g. oral). While most products are designed for exactly one route, there are a few that have more than one route option (Ciprofloxacin drops can be given to eyes or ears), and we will have to handle them in our system.

Even without being able to map the dose, however we are still able to map the drug product from the SNOMED product identifier to the virtual drug-formulation-route which we prescribe with in the hospital.

# Our Workings:
One of the things that went extremely well was that it didn’t take us long to be able to receive data from the EMIS Health test server. EMIS had brought a large team and had set up a working API using GP Connect standards. After a few minor connection issues, we were able to request and receive data for any chosen test patient in under an hour.

Since the GP Connect standards include an HTML (formatted for display) version of the data, we could insert that directly into our application.

With some styling applied, it looks like this:  
![GP Prescription Summary](/img/Hackathon2019/GPConnect_HTML.png){: .center-block :}

With EMIS’s team sitting on the same table as us, we were able to watch as they changed the data to suit our needs, which gave us a better understanding of what different parts of the structured data means.

EMIS were able to adjust their software to pass the dose and frequency in coded form using an example of structured data from Orion health, so that we could play with the data and see how well we could convert it.

With the knowledge that it would be possible to fully match the prescription doses, at least for the majority of prescriptions when the coded dose is passed, we decided to make our solution based on data as it currently stands, using the free text dose and frequency.

We used the FDB Multilex mapping tables to convert the SNOMED product identifier into the FDB product identifier, and then converted it to a virtual drug-formulation-route medication.

We usually prescribe using generic (non-branded) drugs, except when the bioavailabilities differ between brands. The FDB tables include a flag to show when a drug must be prescribed using the branded form, so we are able to map it to the branded drug-formulation-route where necessary.

# Our Solution:
With the drugs mapped to the drug-formulation-route state we use for prescribing, we created an interactive list in the application. The list displays the drug-formulation-route and the free text dose. We realise that we would also need to display the product strength for the dose and frequency to make sense, but for the purposes of the demo we displayed the drug as we would prescribe it.

Since we have mapped the drugs to our drug database, we can identify which of the drugs from the GP system have already been prescribed on our system, and we have added a status flag to the list to demonstrate that.

For the purposes of medicines reconciliation, it will be necessary to match on dose as well, since changes in dose are also sent to the GP in the discharge notification, but until we have dose and frequency in coded form, that will not be necessary. 

Even so, **this is a huge improvement upon manual checking of every drug!**  
![Reconciliation Tab](/img/Hackathon2019/reconciliation_tab.png){: .center-block :}

Even more excitingly, because the drug identified within the FDB multiplex data, **we can warn the user about duplicate ingredients and duplicate therapies and allergy warnings for the patient!**

When a row in the list is clicked, it automatically navigates to the new drug screen. We have displayed the drug product and free text dose and frequency at the top. The selected drug is brought through, so the application can now use our existing decision support functionality (sensitivities, interactions, duplicate ingredients/therapies, and high level warnings).  
![Decision Support](/img/Hackathon2019/decision_suppport.png){: .center-block :}

Over the two days we got to meet people with different areas of expertise, and were able to learn a lot of exciting things about how system interopability is improving. By talking to people from NHS digital, we developed a much better understanding of SNOMED data structure which will help us not just with medicines reconciliation, but also diagnoses and allergies reconciliation.

# The Future
To take this exciting project forward, we are part way through the on boarding process with GP Connect, and we are developing our infrastructure for consuming the data via APIs. Once this is done, we can use some of the workings from our Hackathon days to integrate GP Medications in to our EPMA system, and realise the benefits listed.
