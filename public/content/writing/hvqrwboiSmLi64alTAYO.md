---
title: Scaling Community Engagement
description: By Sreechand Tavva
---
**Context**

Arghyam works with communities that have challenges in accessing safe water from sustainable sources. They either have access to water for a few months a year or they have perennial access to water which is not safe for drinking or domestic use. The NGOs we work with conduct interventions to sensitize communities on

* understanding groundwater

* equipping them to improve their groundwater resources and

* track their resources to ensure sustainability.

The current model is not scalable as the rate at which groundwater depletion is happening in India exponentially surpasses collective efforts of governments, NGOs and CSR initiatives.

### **The Idea**

I’ve noticed that NCERT has incorporated QR codes in their textbooks(Energized Textbooks). These textbooks came with QR codes in each chapter that were linked to videos, experiments and additional problems that improved learning outcomes for students. I’ve also noticed that users are more likely to interact with QR codes on a poster vs when a phone number or a website is provided.

I knew posters can help with sensitization but they lacked the interactive nature in them. The idea was to test if posters can be created that allows NGOs to share content with communities and allow communities to reach out to NGOs.

**The Problem I was trying to solve**

NGOs working on sensitizing communities lack the resources to scale their outreach to sensitize communities dealing with groundwater problems. They use their resources to deliver training in communities that are sensitized or have an active water program. Even though there are a lot more communities that can benefit from this training, NGOs are only able to do training and deliver sensitisation material if they're physically present in these villages. Communities cannot access this material unless they attend a program.

**What made me think of this product**

As a manager at Arghyam, I worked on a few initiatives that enabled NGO partners to start using technology platforms to deliver training online. Their usage increased due to COVID lockdowns limiting their ability to do training in-person. This was a pivotal change as previously skeptical NGOs were now open to piloting newer solutions to their problems.

**What is the product purpose?**

Enable communities to interact with behaviour change material that NGOs disseminate.

**Organizational Objective**

Help NGOs understand the type of water problems that communities are facing without needing to conduct door-to-door surveys.

**Product's features or functionalities**

* Ability to create posters with customizable QR codes that allow NGOs to share relevant videos and instructions.

* Ability for NGOs to find out which training topics were most accessed based on usage tracking data.

* Ability for communications teams to change content linked to a QR code without needing to physically access the poster.

* Ability for communities to get on demand access to updated information on groundwater issues.

**Who are the target stakeholders of the solution?**

* NGOs training communities on groundwater that lack resources to increase their impact.

**Demographics of users**

* Community members

  * in villages with groundwater problems

  * are part of village water committees (address these problems)

  * are comfortable with a smartphone

  * have access to internet.

### **Market Research**

Critical components for this solution are QR code solutions that can

* capture GPS coordinates and

* can tag it to village, district and state boundaries.

I couldn't find any solution that offered both these components at an acceptable accuracy. Most solutions did not capture location but allowed editing the destination URL of the QR code. The rest allowed editing but were priced per QR code making it prohibitive for our stakeholders.

Another challenge was in tagging GPS locations to village, district and state boundaries. Most reverse geo-coding APIs offered by GIS platforms were aimed at providing highly accurate information for cities. They fell short of providing accurate information at village level. They either had stale data (outdated village names, lack of new village boundaries) or served only the closest city/town names through reverse geocoding APIs.

### **Metrics**

The metrics for this project were number of QR code scans by community members and number of posters being deployed. The former gave us usage and the latter adoption.

Usage

* Number of scans for each QR code in a poster

* Number of downloads of content after scanning a QR code

Adoption

* Number of posters deployed monthly

* Number of times NGOs accessed dashboards

* Number of times content on QR codes was edited

### **Prototyping and Design**

I validated this idea at two levels. First was with a mockup to get buy-in from management and the second was with an MVP to get NGOs that wanted to pilot this solution and shape the product.

**Building a prototype**

I built the prototype using Rebrandly (URL shortening service) and simple static QR code generator. Rebrandly allows edits to the source and the destination URL. I created a poster with content from an existing material. I added a few QR codes that were pointed to videos. I scanned the QR code along with using a GPS spoofing app to increase scans for different QR codes in two different villages. I exported this data, and used Google Maps reverse geocoding API to capture the village of each scan. I plotted this in a custom google map and added it to the table of scans and location for scans.

**Building the MVP**

Building the MVP needed a few more hands on deck. Having got approval to test MVP, I got an NGO partner to design a poster and share material that they wanted to embed. Using the QR code solution by [Beaconstac](https://www.beaconstac.com/) I embedded them with QR codes pointing to videos, PDFs and forms. I shared this poster with my team and instructed them to scan them while at the office and on their field trips. With the reverse geocoding API I got village names for each scan and put them in tables along with a map of the scans. I demoed this to a few NGOs and got two of them to pilot the product.

### **Product Architecture**

* Notion for the content team to create public pages

* Google Drive to upload files and videos.

* [QRD.by](https://qrd.by/) for generating QR codes and capturing GPS coordinates

* A DigitalOcean server hosting the db and scripts to call reverse geocoding APIs by MapMyIndia (replaced with a GIS server from [FES](https://www.fes.org.in/))

* Google Data Studio Dashboard with 6 charts

**\
Future Plans, product enhancements**

* Two NGOs are using this product. Future plans involve scaling marketing and onboarding more NGOs to make the product self-sustainable.

* Current dashboards are not customizable by an NGO. Plans in the pipeline are to use a BI tool that allows customization.

### **Challenges**

* Reverse geocoding GPS coordinates from QR codes uncovered that village names were highly inaccurate. I compared MapMyIndia, Google Maps and OpenStreetMaps and settled on MapMyIndia.

* The person sending the posters with QR codes is different from the ones editing content on it. A prior version relied on the poster creator and content editor being the same person. It relied on the poster creator generating unique QR codes for each poster.

* The first version of the product used APIs from MapMyIndia. After building it using a developer API key, and requesting for a production API key, they came back with a restriction that the agreement does not allow caching of the reverse geocoding API results. One of the two NGO partners had a GIS server with reverse geocoding API, their results met our accuracy needs, we switched to their APIs.