
# MIST 4610 Group Project 1: Mr. Treest

## Team Name - 21482 Group 3

Team Members:
- Tyson Elmore [@TysonElmore](https://github.com/TysonElmore)
- Matthew Liu [@marshy6](https://github.com/marshy6)
- Lucas Luxemburger [@lucasjbluxemburger](https://github.com/lucasjbluxemburger)
- Gabe Po [@gabepo](https://github.com/gabepo)
- Chris Trinh [@cat35795](https://github.com/cat35795)

## Scenario Description


 
## Data Model

The model is structured around how the organization manages its programs, donations, volunteers, and the communities it serves.

The Donor entity represents individuals or organizations that contribute financially. Each donor may make multiple donations over time, which is why there is a one-to-many relationship between the Donor and Donation entities. The Donation entity stores information such as the amount and date of each contribution and may optionally be associated with a specific Program, allowing the organization to track which initiatives are being funded.

The Program entity represents major tree-planting initiatives. Each program has attributes such as a name, start and end dates, and a goal number of trees to be planted. A program can consist of many Planting Events, so there is a one-to-many relationship between Program and PlantingEvent, where each event represents a specific date that trees are planted.

There are two branches that come from the Program entity. First, the ProgramCommunity entity represents the relationship between programs and the communities they serve. Because a program can serve many communities and a community can benefit from many programs, there is a many-to-many relationship between Program and BeneficiaryCommunity, which is resolved through the ProgramCommunity associative entity. This table also stores additional information such as the estimated number of residents served.

On the other branch, the PlantingEvent entity connects to the operational side of the organization. Each planting event occurs at a specific Site, and each site belongs to a single BeneficiaryCommunity, resulting in a one-to-many relationship between BeneficiaryCommunity and Site. Communities themselves are structured hierarchically, as a community may contain subcommunities, which is represented by a recursive one-to-many relationship within the BeneficiaryCommunity entity.

Each planting event results in multiple Tree records, creating a one-to-many relationship between PlantingEvent and Tree. Each tree is associated with a TreeSpecies, which stores information such as the common and scientific name of the species. This creates a one-to-many relationship between TreeSpecies and Tree, as each species can correspond to many individual trees.

Additionally, the model captures the lifecycle of trees through a recursive relationship within the Tree entity. A tree may be replaced by another tree, and each replacement tree corresponds to only one original tree, forming a one-to-one recursive relationship that allows the organization to track replanting efforts over time.

Volunteers play a key role in operations. The Volunteer entity represents individuals who participate in planting events. Volunteers can work at many planting events, and each planting event can involve many volunteers, so there is a many-to-many relationship between Volunteer and PlantingEvent. This relationship is resolved through the VolunteerAssignment associative entity, which also stores additional details such as the volunteer’s role and hours worked during each event. The VolunteerRole entity defines the different roles that volunteers can perform.

Each volunteer must also have a background check record, which is represented by the VolunteerBackgroundCheck entity. This creates a one-to-one relationship between Volunteer and VolunteerBackgroundCheck, ensuring that each volunteer has exactly one associated background check record.

Lastly, the Site entity represents physical locations where trees are planted. Each site belongs to a single community, but a community can have many sites, reinforcing the one-to-many relationship between BeneficiaryCommunity and Site.

<img width="856" height="749" alt="image" src="https://github.com/user-attachments/assets/adb2615b-b50f-402f-9091-c5b9a167c91c" />

## Data Dictionary

<p>
<img width="742" height="326" alt="image" src="https://github.com/user-attachments/assets/87633093-9288-4f6e-b983-a641f2927cda" />
<p>
<img width="736" height="286" alt="image" src="https://github.com/user-attachments/assets/ddceb9cd-d85d-4dbe-8f7b-71bb92a69781" />
<p>
<img width="731" height="186" alt="image" src="https://github.com/user-attachments/assets/bebba9e7-f84b-4cd3-8ccd-fa1dc6e8d261" />
<p>
<img width="730" height="206" alt="image" src="https://github.com/user-attachments/assets/0bede992-f645-4f37-8529-15939d70c16e" />
<p>
<img width="719" height="206" alt="image" src="https://github.com/user-attachments/assets/1f68c8e7-5b11-4214-af03-b2998371e8e4" />
<p>
<img width="820" height="186" alt="image" src="https://github.com/user-attachments/assets/cbe980d8-9b1e-48d3-916c-f128a7e903da" />
<p>
<img width="742" height="306" alt="image" src="https://github.com/user-attachments/assets/7aa820ba-d9d0-4c77-8816-c38a7bd893e4" />
<p>
<img width="762" height="346" alt="image" src="https://github.com/user-attachments/assets/7c141c17-2f98-4232-84af-feb534ccb047" />
<p>
<img width="715" height="146" alt="image" src="https://github.com/user-attachments/assets/63882e08-81f3-403e-8b1b-7b337bd2d862" />
<p>
<img width="721" height="206" alt="image" src="https://github.com/user-attachments/assets/314e9390-b46f-47ef-9fd6-eb1dcb513d4c" />
<p>
<img width="767" height="246" alt="image" src="https://github.com/user-attachments/assets/9c2cb9e8-d6bc-4304-be7d-af2d1c0fd3a6" />
<p>
<img width="742" height="226" alt="image" src="https://github.com/user-attachments/assets/6717b115-62aa-48dc-ba33-b1ff5fc91c6b" />
<p>
<img width="715" height="126" alt="image" src="https://github.com/user-attachments/assets/accb84a3-7081-4618-a663-b51ee7a167b2" />
</p>

## Queries

### Query 1: Total donations by program 

Query 1 shows how much each organization has donated to our nonprofit. It is not in any specific order (ex. largest to smallest) but has the companys name and amount that they have donated

<img width="959" height="349" alt="Screenshot 2026-03-30 at 2 12 37 PM" src="https://github.com/user-attachments/assets/7012d7c7-5bd2-480c-acd7-a1ae22165abb" />

This helps management evaluate which programs are most successful in attracting donations, allowing them to prioritize funding efforts and allocate resources more effectively.  It also makes it easier to track donation goals, making it possible to set a goal for a company and if they hit it they can have a section of replanted trees names after them. 

### Query 2: ... 
(description)

<img width="895" height="409" alt="Screenshot 2026-03-30 at 2 14 59 PM" src="https://github.com/user-attachments/assets/eef226d3-ea1b-4161-a16b-4fbbe324e623" />


This allows managers to identify highly engaged volunteers, recognize top contributors, and make decisions about rewards, promotions, or leadership opportunities.

### Query 3: ... 
(description)

<img width="890" height="337" alt="Screenshot 2026-03-30 at 2 17 11 PM" src="https://github.com/user-attachments/assets/9cf75fbb-567a-48ac-83d9-86bd48e93e82" />

This helps managers assess the productivity and effectiveness of individual planting events and improve planning for future events. 

### Query 4: ... 
(description)

<img width="894" height="322" alt="Screenshot 2026-03-30 at 2 24 24 PM" src="https://github.com/user-attachments/assets/0f8d0794-a000-4649-ac5d-344decd1b830" />
 
This provides insight into geographic coverage and helps managers identify underserved areas or opportunities for expansion.  

### Query 5: ... 
(description)

<img width="889" height="442" alt="Screenshot 2026-03-30 at 2 26 43 PM" src="https://github.com/user-attachments/assets/e3e0a3d3-57a0-461b-b4ad-5cc57415e25b" />

This helps management identify top-performing programs financially and understand which initiatives are most attractive to donors. 

### Query 6: ... 
(description)

<img width="894" height="322" alt="Screenshot 2026-03-30 at 2 24 24 PM" src="https://github.com/user-attachments/assets/832ef402-930a-4ac9-8096-901f57070ef1" />

This allows managers to evaluate and compare environmental impact across all communities, helping them identify which areas are performing well and which may need additional focus or resources.

### Query 7: ... 
(description)

 <img width="989" height="655" alt="Screenshot 2026-03-30 at 2 29 13 PM" src="https://github.com/user-attachments/assets/07504c3a-b0d3-4318-96bd-69781d071266" />

This helps managers identify exceptional volunteers and understand engagement levels, which can guide retention strategies and volunteer recognition programs. 

## Database Information

### Query 8: ... 
(description)

 <img width="733" height="378" alt="Screenshot 2026-03-30 at 2 30 31 PM" src="https://github.com/user-attachments/assets/805feb9c-a906-4b21-a283-8ab12caa35c3" />

This highlights operational issues in event planning and staffing, allowing managers to address gaps and ensure future events are properly supported.

### Query 9: ... 
(description)

<img width="988" height="602" alt="Screenshot 2026-03-30 at 2 31 40 PM" src="https://github.com/user-attachments/assets/386e2128-678e-43c3-b6eb-4c222d3cb38e" />

This helps managers evaluate the efficiency of events by comparing output (trees planted) to input (volunteer hours), allowing them to improve planning, allocate resources more effectively, and replicate high-performing events.  

### Query 10: ... 
(description)

<img width="994" height="500" alt="Screenshot 2026-03-30 at 2 32 47 PM" src="https://github.com/user-attachments/assets/33ea7e1b-dca5-417d-ac23-af99f22e8fe7" />

This helps identify highly valuable donors who are deeply engaged with the organization, allowing for targeted relationship management and fundraising strategies. 

## Database Information

