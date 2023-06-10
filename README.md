# Wound-Classifier


# Wound classification using resnet CNN

This is an attempt to reproduce the work of this excellent paper: https://www.nature.com/articles/s41598-022-21813-0

The dataset is from the AZH Wound and Vascular Center in Milwaukee, Wisconsin. It is published here: https://github.com/uwm-bigdata/Multi-modal-wound-classification-using-images-and-locations/tree/main/dataset

# Discussion of Clincal Use

<sub>*Summary:*<sub>
- <sub>*Use it in EHRs to suggest coding*<sub>
- <sub>*Use it to populate clinical reminders*<sub>
- <sub>*Use it in direct-to-patients apps* <sub>





## What clinical good is wound classification? 
Having a DL model of wound classification would be an amazing tool. 
However, just using a it to put a label on a wound is not very useful clinically.  Most clinicians are competent to determine the underlying pathology of a wound.  Even when unsure, clinicians are likely to make a more accurate assessment based on patient history rather than relying solely on a wound classifier's interpretation of an image.  In reality, most wounds exist along a spectrum. For example: diabetic wounds that are also pressure ulcers or vascular wounds that are mixed venous and arterial insufficiency.  

Can the classifier be helpful in guiding treatment?  Probably not very much.  The main question in treatment choice is often not "What is recommended?" but "What is covered by insurance?"  Fortunately, for any given wound there are usually many possible successful wound care protocols.  The basic principles of dressing a wound apply to wounds of all origins:
- Keep it moist
- But not too moist
- Keep it clean  
- Get rid of dead tissue
- Keep the pressure off
- Nutrition!

Most clinicians who see wounds on a regular basis have a few favorite "go-to" regimens that they try first. That is unlikely to be changed by a classifier. 

## So how can this technology fit into practice?
Providers don't really need help with know what a wound is or how to treat it. 
What providers **DO** need help with is the overwhelming amount of adminstrative burden involved in care.  At its best, health tech should lessen that burden and smooth the path for clinicians to focus on the patient and clinical decision making.  The administrative burdens involved in wound care are:
- Coding
- Documentation
- Ordering wound care supplies
- Care gaps


## Coding: 

Let's start with coding, since coding is the area where a wound classifier could really shine. 

There are hundreds of ICD 10 codes for wounds.  Imagine a typical older patient: 75 year old female obese, diabetic, smoker, with peripheral vascular disease.  Imagine she has developed a sore on the outside of her left foot, reaching from the side of the heel to just below the ankle.   Here are a few valid ways you could code that:
- L89.529 Pressure ulcer of left ankle, unspecified stage
- L89. 622 Pressure ulcer of left heel, stage 2 
- E11. 621 for Type 2 diabetes mellitus with foot ulcer 

A trained medical coder could read that description and tell you that it should be coded as specifically as possible, that you should code any ischemia in the wound first, and that you should exclude infected or diabetic wounds from a pressure ulcer coding, but a clinician has about 2 seconds in a 30 minute visit to make the decision of which code to pick.  Confusing matters, each ICD 10 code has several dozen descriptors, so when I start to type a description "Wound, Left foot" into the search bar of my EMR software's ICD 10 library, I can scroll through dozens and dozens of ICD 10 options with that description. 

How a classifier could help: A classifier could know the ICD 10 rules and present the most likely option as a default ICD 10 to choose if the clinician agrees with it. 


### Documentation: 
Solutions are already developed for smoothing documentation.  Epic app orchard, for the the 30% of doctors in the US who are on Epic, has a few apps which use an image of a wound to automatically populate the note with measurements and save the image to the chart.  Outside Epic, products such as this: https://www.tissue-analytics.com/  are popping up which can also do this (and probably much more accurately than humans).   At this point, getting these tools into daily use for all the interactions where wounds are being treated across the country is a problem for implementation science:  https://www.sciencedirect.com/science/article/pii/S016517811930602X

 


## Ordering wound care supplies:
Wound care supplies are ordered from DME (durable medical equipment) companies and paid for by the patient's insurance.  DME companies need documentation in order to bill the insurance.  They need a clinical note, an order, and wound measurements.  Most DME companies require not just your visit note, but their own form filled out and signed by the provider. If you are lucky, the DME company pre-fills the form with whatever you ordered and there is a single, clearly visible line for you to sign and date.  If you are not lucky, you get a blank, densely printed form in tiny font with dozens of options, where you have to search for where to write the wound measurements and where to sign.  Having to fill these forms out requires opening up the patient's last visit note and finding the wound measurements.  Each task only takes a few minutes, but multiply these tasks over and over each day, and you get a significant amount of time spent that clinicians are just doing data entry. 

Intelligent fax handling already exists, that can read PDFs, enter some prefilled information.   This is less a task for a classifier, and more a task that needs implementation of existing tech and connections of EMRs to tools that can do PDF handling. 


## Care gaps: 
Care gaps are the appropriate "To Do" list for patients based on their diagnoses.  For example, a patient who has a wound that could have some ischemic component should get arterial dopplers and a referral to vascular to see if there is a chance of getting a stent in their artery to restore blood flow to the leg.  A patient with a diabetic ulcer should receive diabetic education and med adjustments to get their HA1C down to a good range.  Clinicians know these steps, and in an ideal world, have the time, resources, and patient / family cooperation to get them done. In the real world, visits can be chaotic.  I work in home care.  In some visits involving wounds, the wound is the focus of the visit.  I spend time talking with the family about what protein supplements to buy and how to wedge pillows under the hip to take the pressure off the sacrum.  I call the nurse and discuss dressings.  In other visits, the focus of the visit is poverty, hoarding, family violence, mental health, extreme poor hygiene, alcoholism, or other very urgent matters, and the wound is way down on the list of things the patient is worried about.  In those visits appropriate care gap follow up can be hard to focus on.  A wound classifier can help by populating the visit note with reminders based on the wound category.  For example, a wound that classifies as a diabetic ulcer could populate a reminder to order a CRP and Xray to evaluate for osteomylitis.

# Power to the people
AI and health tech has the power to be incredibly effective in reducing bad outcomes over large populations by getting a lot of the work of care out of provider's hands by directly empowering patients and families. 

## Preventable wounds 
Some wounds happen even in ideal circumstances.  A patient who is 102 can be lovingly and meticulously cared for, but the skin, like all organs, can just fail.   Many wounds, however, are behaviorally based.  We all sometimes do things that aren't good for us; as our bodies get more frail, those bad habits tip over into the realm of causing major problems.  Here are habits that can result in non-healing wounds: sitting with legs down all day, smoking, skipping meds, wearing ill-fitting shoes, sitting in a wet adult diaper, drinking soda, or eating salty food.   

Intelligent tech can help behavioral change by putting the power in the hands of the patient or caregiver.  Imagine a wound classifier built into a consumer tech app.  A family member can snap a picture of a wound forming on grandma's backside, and get a list of suggestions for changes that can improve the wound (maybe even Amazon links to Juven and wedge pillows).  They can image the wound daily and get rapid feedback if what they are doing is working.  A patient with venous stasis wounds can get alarms if they sit with their feet down for too long.  A patient with a diabetic wound can get instant education on how their wound is connected to their blood glucose.  

## Tech as Public Health 
Knowledge passes from research to clinical practice, to popular use, and finally to established culture.   In the 1860's Louis Pasteur was dunking glass vials of milk in boiling water, then a few years later Joseph Lister was making all his students wash their hands with carbolic acid between surgeries.  Now we all wash our hands after using the bathroom, and I personally don't know anyone who has died of cholera.  

Just yesterday I visited a patient who is developing a vascular wound on his leg.  He found it almost impossible to believe that the wound was a result of the smoking, and most of our visit was me trying to explain it.  My hope is that knowledge that right now lives in the realm of health care can soon be common knowlege, and even more importantly, common **practice**. 
I can imagine a time when a wound classifier is part of direct tech that monitors and assesses all aspects of health, offering education, behavioral interventions, rapid feedback, and guidance.  



