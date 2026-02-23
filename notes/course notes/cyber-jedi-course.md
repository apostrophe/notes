
url: https://ikea.csod.com/ui/lms-learning-details/app/course/ce4e96d2-63de-465d-86eb-5bac6a041a3f?isCompletionRedirect=true


Cyber Jedi community: a global network of people who champion security and privacy across the organisation. This community focuses on growing awareness, sharing practical knowledge, and providing hands-on guidance to help teams embed cyber security and privacy into their daily work. 

blameless culture—one where curiosity, transparency, and learning from mistakes are encouraged

Why it's important:

• Protecting Our Customers: Ensuring the safety of our customers' data and personal information is paramount. A strong security posture helps maintain their trust and loyalty. 

• Safeguarding Our Brand: Security breaches can damage our reputation and financial standing. By prioritizing security, we protect IKEA's brand integrity. 

• Compliance and Regulations: Adhering to security standards and regulations is essential to avoid legal repercussions and ensure smooth operations. 


Your Role:

• **Stay Informed**: Keep up-to-date with the latest security practices and threats. Knowledge is your first line of defense. 

• **Report Suspicious Activity**: If you notice anything unusual, report it immediately. Early detection can prevent potential breaches. 

• **Adopt Best Practices**: Implement security best practices in your daily tasks. Simple actions like using strong passwords and being cautious with emails can make a big difference. 

• **Collaborate and Share**: Work together with your colleagues to create a secure environment. Share insights and support each other in maintaining security standards. 

• **Contacts with Cyber Security & Privacy**: As you level-up in Cyber Security, we want to know who can help support our Cyber Journey.  


### Cyber Journey
Inventory
Ranking - impact to business
  bronze
  silver
  gold
  platnium
Fundamtnals
  70 controsl that are required for s ecure system
Measure

Automatic Compliance

---------------------------------------------
The overarching structure of the Cyber Journey is made up of 4 parts: 

• Inventory: Making sure that our systems and system components are inventoried 

• Classifying: This is the classification introduced in the Metal Model, making sure that we understand the impacts if a system is breached and to serve as a coarse prioritization schema.  

• Fundamentals: Addressing the fundamental security & privacy requirements that will protect our systems to avoid negative business impacts 

• Measure: Measuring and helping teams know where they are in securing the product and monitoring to see where we can make improvements. 
---------------------------------------------


The Classification is based on:

Data Sensitivity: How confidential and important the data is. 

System Availability: How crucial it is for the system to be up and running without interruptions. 

Compliance: Ensuring the system meets legal and financial regulations. 

Business Impact: How critical the system is to the overall business operations. 


### Access 
- Access to metal model is managed by the [teams in Allen](https://allen.ingka.com/home?ingka_teams_modal=true)  
- The 'Connected Teams' in metal model -> Allen https://metal-model.ingka.com/userSystems  
- Instructions on connecting team to metal model (**this might need to be done in System Master Catalog**): https://confluence.build.ingka.ikea.com/spaces/SYSCAT/pages/533606895/Connect+Team+to+System

### Incident Reporting
https://iweof.sharepoint.com/sites/cybersecinc/SitePages/sv/Home.aspx
There's an option to report anonymously 

The types of incidents could be (but are not limited to):
- Customer Data Breach
- Coworker Data Breach
- Phishing or other scam e-mail
- Brand Impersonation Scam
- Compromised website, server, or IT infrastructure

### Connect SMC to Cloud Account
https://confluence.build.ingka.ikea.com/pages/viewpage.action?spaceKey=CYBERSEC&title=Cloud+Portal+-+Relate+%28SMC%29+System+to+Cloud+Account

### Cloud Security Alerts
Krishnapriya - Cyber Engineer


### Workload Placement
https://confluence.build.ingka.ikea.com/spaces/CF/pages/1022818156/Workload+Placement

*** [**Ingka-Specific Guidance**](https://allen.ingka.com/docs/default/Component/ea-workload-placement/workload-placement/) ***



Further reading:

Ingka, Workload Placement, https://allen.ingka.com/docs/default/Component/ea-workload-placement/workload-placement/
Google, Hybrid and multicloud architecture patterns, https://cloud.google.com/architecture/hybrid-multicloud-patterns-and-practices
Google, Google Cloud deployment archetypes, https://cloud.google.com/architecture/deployment-archetypes
Google, Choosing a network connectivity option in Google Cloud, https://cloud.google.com/blog/topics/developers-practitioners/choosing-network-connectivity-option-google-cloud/



### SSO
https://allen.ingka.com/platforms/product/identity-authentication/self-service



[ ] links on cloud portal page (education, )


### Pen Testing
- only applied to platnium applications
- annual cadence


### Privacy
engineers need a privacy mindset
Core privacy principles:
- Minimization: Only collect what you really need. Avoid the “we might need it later” trap or “the more the better”. 
- Purpose limitation: Be clear on why you’re collecting data and don’t reuse it for something else without consent. 
- Security/privacy by design: Encrypt, anonymize, and secure data from the first line of code. 
- Transparency: Make it easy for users to understand what’s happening to their data. 
- User rights: Support deletion, access, and correction of data in your systems. 

engineers need to understand: 
- What personal data looks like in your codebase 
- What a privacy risk is 
- How to spot (and prevent) one in your design 

### Questions - Fika with Security Engineer
- Beaulah-Rachel (sales planning, (something else): 
  - come up with security guidelines
  - is there anything that teams do to ensure that high and critical errors get resolved (and not just assume they'll get patched in a package manger (npm, gradle, etc))?
    - best, most up-to-date list for critical & high vulnerabilities:
      - metal model <-
      - cloud account <-
      - github/dependabot (only patches?) <-
      - 
  - attack-forge - that's only for cyber teams, correct? yes, pen testing
  - any tasks you recommended teams do in the early stages?
  - i'm being asked to create a security strategy -- any templates you'd recommend? -> cyber journey has taken place, cyber team can assist priority
  - [there are these documents where the cyber team reviewed all of the teams disaster recover play, 2 others. how do we get added to that group? when do you recommedned us planning for our first review?]
  - risk reports - release every tertial - how do they relate to teams
    https://confluence.build.ingka.ikea.com/spaces/CYBERGOV/pages/492357809/Cyber+Risk+Reports -> if anything in report relates to component of our project, it should open further discussion with security team
  - GDPR all covered by 'privacy by design' assessment? yes
    - there is privacy engineer: guillermo.iribarren@ingka.ikea.com
  - Any tempaltes for security strategy? No, we use metal model.



# Define Recommendations for Engineer Reading or Cyber Jedi Courses
https://jira.digital.ingka.com/browse/SSPLAN-143

Purpose of ticket: what training should engineers have around security/privacy?
1. Cyber Jedi - Level 1 Padawan - basic knowledge of security and privacy at IKEA
2. Any links that you'd recommend reading?
  - Secure SDLC
  - others?

What should we be doing and keeping in mind as we develop this application in order to ensure the appliation is secure and protects PII?
 - what minimum knowledge should all engineers on the team have to ensure we are following secure best practices 

Truthfully, I don't know if that captures everything. What should we be doing as we develop?
Between the definitions of done and the metal model, which should shore up any practices we aren't doing regularly, we should capture everything. 
Are there any confluence pages that should be reviewed?
Review what's on the EB Security page.

We are taking this from the perspective of the engineers. What is important to know about security and pii at IKEA? 
- Consider changes we make and how they could impact the security of the application
- Include the security concerns when reviewing code
- Be familiar with how the ikea cyber - cyber jedi course
- Be familiar with how important PII is at IKEA
- SDLC Security cycle
- Particular vulnerabilities in our working environment (current threat environment, cloud-specific risks, CW and Customer PII)

 should they know regarding. I don't want to second guess what has already been determined to be recommended, but I can supplement what they have in course 1.
 
[x] Is taking course 1 overkill? Is it necessary for each of engineers to take it? How do I defend taking it? There won't be an enforcement required on my part, so I shouldn't worry too much about this. 
Defend: It's a good baseline
I would recommended all of the engineers take it to understand. 
It should take only 1-2 hours.
[ ] find links around coding and code reviews with security in mind
[ ] does the metal model define secure SDLC? there's a page on it
[ ] review everyting covered in courses1,2,3 and determine whether we need to create tickets for them
discuss with team: creating 
[x] are there metal model controls to handle code/package scans? Yes

Lower Priority
[ ] Does the cyber jedi course 1 mention taking a security-first approach? I'm not sure that it does, but either way, this is a lower priority.
[ ] Is there anything in the jedi course 1 that we should be including in recommednations/plan for T2 or beyond? -> To review later
  Cloud Security Alerts


---------------------------------------------------------------------------
It's not clear until you start the courses what they cover, so I'm providing a summary below.

  # Cyber Jedi Courses

  Level 1/Padawan is a general overview of security and privacy practices at IKEA. 
  Levels 2 & 3 (Knight and Master) are more in-depth exercises used to further secure the system under developement. 

  - Level 1/Padawan
    - What are Security Threats?
    - OWASP Top 10
    - Cyber Security at Ingka
    - How do I report an incident?
    - With Cloud comes Great Power
    - Cloud Misconfiguration
    - Security Principles
    - Offensive Security Testing
    - Resilience
    - Understanding SSO & Access Management
    - Why Privacy matters at Ingka
    - Cyber Security External Content

  - Level 2/Knight
    1. [OWASP Top 10:2025](https://owasp.org/Top10/2025/) - You're asked to choose one of the OWASP Top 10 to learn about and apply the recommendations to mitigate the security risks.  
      a. Also recommended: [Top 10 Proactive Controls](https://top10proactive.owasp.org/)
    2. Language/stack-specific security guides - You're asked to review security guidelines based on the language/stack being used:
        - Example: [Kotlin Guide](https://confluence.build.ingka.ikea.com/spaces/SSEC/pages/118579022/Kotlin) 
    3. [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks) -- external product

  - Level 3/Master
    1. Threat Modeling - A guide for how to create a threat model for your application
    2. Static Application Security Testing (SAST) and Software Composition Analysis (SCA) 
    3. Cloud-specific security courses
      [Google Cloud Platform Fundamentals(pluralsight)](https://app.pluralsight.com/id/?redirectTo=/library/courses/google-cloud-platform-fundamentals/)
      [Managing Security in Google Cloud Platform(pluralsight)](https://app.pluralsight.com/id/?redirectTo=/library/courses/managing-security-google-cloud-7/table-of-contents)
    4. Secure Application Guideline Activities (SAGA) - this section is a guide for managing secrets across the SSDLC
    5. Managing Security Flaws - Recommendations found [here](https://confluence.build.ingka.ikea.com/x/NaZjD) that they're asking feedback on, although from 2020.




It's going to be more of a priority once we start building things, we have the metal model and PII 

I would say the most important thing to think about is, for any of the below changes, do we need to investigate anything. And even if it's just a question (do we need to worry about X?) raise the question, creating a ticket to investigate is better than not addressing it and having it come up later.
- in code and configuration changes, 
- in code reviews
- integrating with new systems
    - consider data retreived or sent to another system
    - how it's accessed (data in motion, in use, at rest)
      - in motion: transmitted to another system
      - in use: pulled into the front end 
      - at rest: stored in db, 
    - how it's stored, who has access)


SSPLAN-144 - Review Definition of Done for Alignment with Security Best Practices
https://jira.digital.ingka.com/browse/SSPLAN-144


1. Code Complete
- any changes made, security and privacy implications have been considered.
or maybe
- code follows 
5. Deployable 
- and changes made to

7. Security & Compliance (for all stories that have implementation changes)
Any code changes that update PII shoud be raised and considered for a change to the Privacy by Design assessement. 




