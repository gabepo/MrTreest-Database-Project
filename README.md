
# MIST 4610 Group Project 1: Mr. Treest

## Team Name - 21482 Group 3

Team Members:
- Tyson Elmore [@TysonElmore](https://github.com/TysonElmore)
- Matthew Liu [@marshy6](https://github.com/marshy6)
- Lucas Luxemburger [@lucasjbluxemburger](https://github.com/lucasjbluxemburger)
- Gabe Po [@gabepo](https://github.com/gabepo)
- Chris Trinh [@cat35795](https://github.com/cat35795)

## Scenario Description

The objective of this project is to design and implement a relational database that models the operations of a tree-planting nonprofit organization, the Mr. Treest Tree Planting Non-Profit Organization (MTTPNPO). The central focus of the model is on programs and planting events, which represent the organization’s efforts to plant trees in underserved communities and improve environmental sustainability. These programs are supported by donor contributions and carried out through volunteer participation at various planting sites. The database is designed to capture the relationships between donors, donations, programs, communities, volunteers, and planted trees. We aim to accurately model these relationships, generate sample data, and populate the entities with this data. This enables us to perform queries on the database that provide meaningful insights into funding, volunteer involvement, and the overall impact of the organization’s activities.
 
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

<img width="988" height="857" alt="MrTreestDataModelPNG" src="https://github.com/user-attachments/assets/1456ff4f-8629-48cb-ae37-1d5722a5531f" />

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

<img width="1103" height="212" alt="image" src="https://github.com/user-attachments/assets/ec3062d2-2878-459d-be64-d28a22599d64" />

### Query 1: Total donations by program 
How much total funding has each program received?
- Query 1 shows how much total funding each program has recieved. It is not in any specific order (ex. largest to smallest) but has the program name and total amount donated. 

<img width="959" height="349" alt="Screenshot 2026-03-30 at 2 12 37 PM" src="https://github.com/user-attachments/assets/7012d7c7-5bd2-480c-acd7-a1ae22165abb" />

- This helps management evaluate which programs are most successful in attracting donations, allowing them to prioritize funding efforts and allocate resources more effectively.  It also makes it easier to track donation goals. 

### Query 2: Total Volunteer Hours by Individual
Which volunteers have contributed the most total hours?
- Query 2 shows how many hours an individual has dedicated to the movement. It has their first and last names, and then how many hours they have served. 

<img width="895" height="409" alt="Screenshot 2026-03-30 at 2 14 59 PM" src="https://github.com/user-attachments/assets/eef226d3-ea1b-4161-a16b-4fbbe324e623" />

- This allows managers to identify highly engaged volunteers, recognize top contributors, and make decisions about rewards, promotions, or leadership opportunities. It allows people who are earning hours for community service to easily track their hours, and could incentivize others if we said we were rewarding the top 5 best volunteers. 

### Query 3: Trees Planted per Event
How many trees were planted at each event?
- Query 3 keeps track of how many trees were planted at a given event. It tracks the number of trees that were planted and what the event was called. 

<img width="890" height="337" alt="Screenshot 2026-03-30 at 2 17 11 PM" src="https://github.com/user-attachments/assets/9cf75fbb-567a-48ac-83d9-86bd48e93e82" />

- This helps managers assess the productivity and effectiveness of individual planting events and improve planning for future events. This gives us an organized bank to account for how many each trees were planted at that event. 

### Query 4: Sites Organized by Community
Which sites are located within each community?
- Query 4 shows what communities we have helped and the site where the trees were planted at. This allows us to keep tabs of where we need to put our focus after we have helped the communities around us.  

<img width="894" height="322" alt="Screenshot 2026-03-30 at 2 24 24 PM" src="https://github.com/user-attachments/assets/0f8d0794-a000-4649-ac5d-344decd1b830" />
 
- This provides insight into geographic coverage and helps managers identify underserved areas or opportunities for expansion. This will allow for an even distribution of trees around the area that we are assisting. 

### Query 5: High-Funding Programs
Which programs have received a high level of total donations?
- Query 5 helps us track each company by keeping track of what their goal for trees planted and amount of money donated to make that possible.  

<img width="1238" height="378" alt="image" src="https://github.com/user-attachments/assets/7a4339a2-9a23-4722-8155-983638e55098" />

- This helps management identify top-performing programs financially and understand which initiatives are most attractive to donors. Each program is allowed to set their own goals for themselves and be able to track their donation goal.  

### Query 6: Communities by Total Trees Planted
How many trees have been planted in each community?
- Query 6 shows how many trees have been planted in each community and location that the donations went towards. With the site name prompted next to which community the trees were planted. 

<img width="894" height="322" alt="Screenshot 2026-03-30 at 2 24 24 PM" src="https://github.com/user-attachments/assets/832ef402-930a-4ac9-8096-901f57070ef1" />

- This allows managers to evaluate and compare environmental impact across all communities, helping them identify which areas are performing well and which may need additional focus or resources. Keeping track of where we are planting trees makes it simpler to figure out where the next projects should be at. Allowing the whole community to be rewarded. 

### Query 7: Volunteers Exceeding Average Hours
Which volunteers have worked more hours than the average volunteer?
- Query 7 showcases the number of volunteers that have clocked more hours than the average volunteer. It shows the particpants name, total hours worked, and the average hours worked from other volunteers.  

 <img width="989" height="655" alt="Screenshot 2026-03-30 at 2 29 13 PM" src="https://github.com/user-attachments/assets/07504c3a-b0d3-4318-96bd-69781d071266" />

- This helps managers identify exceptional volunteers and understand engagement levels, which can guide retention strategies and volunteer recognition programs. Can be acknowledged and entered monthly raffles for rewards to incentivize people to commit more hours to the cause. Since we are running a nonprofit, volunteer hours are very important as well as people who are committed to the movement. 

### Query 8: Events Without Volunteer Assignments
Are there any planting events this year that did not have any volunteers assigned?
- Query 8 shows events that would pop up if no volunteers signed up for them. The code does not return any eventId's or eventDate's right now because all events have volunteers. Also included is an AND statement which is part of the multi condition WHERE statement. This AND is an example additional condition filtering by date, so management can see which events on certain dates don't have any volunteers. We use "2026-01-01" as an example. 

 <img width="1243" height="422" alt="image" src="https://github.com/user-attachments/assets/1f03d5e3-2c78-4ea8-b0d6-17df02ebe88f" />

- This highlights operational issues in event planning and staffing, allowing managers to address gaps and ensure future events are properly supported. It will be very useful to operations, especially when there are more programs and multiple events happening each week. This will ensure that no events are understaffed or run poorly.  

### Query 9: Event Efficiency (Trees per Volunteer Hour)
Which planting events were the most efficient in terms of trees planted per volunteer hour?
- Query 9 identifies which planting events were the most efficient in terms of trees planted per volunteer hour. Listed are programs, trees planted, total hours spent working and then calculated is the trees per hour. The list is in descending order from most trees an hour to least.  

<img width="988" height="602" alt="Screenshot 2026-03-30 at 2 31 40 PM" src="https://github.com/user-attachments/assets/386e2128-678e-43c3-b6eb-4c222d3cb38e" />

- This helps managers evaluate the efficiency of events by comparing output (trees planted) to input (volunteer hours), allowing them to improve planning, allocate resources more effectively, and replicate high-performing events. This data is important on showing what kind of system works the best to make sure that efficiency is at the maximum. In addition, this data is not always the most reliable, because not every event will have the same number of volunteers.  

### Query 10: Multi-Program Donors
Which donors with the last name 'Lopez' have contributed to more than one program?
- Query 10 identifies donors who have contributed to more than one program and whose last name matches a specified pattern (in this case, last names beginning with “Lopez”). It returns the first name, last name, and donor ID for these qualifying donors.

<img width="990" height="484" alt="Screenshot 2026-03-30 at 6 02 21 PM" src="https://github.com/user-attachments/assets/bcbcfd75-5aab-4036-9347-1ec550dd5c43" />

- This query helps identify highly valuable donors who support multiple programs while also allowing for targeted segmentation based on naming patterns. This can be useful for personalized outreach, demographic analysis, or creating targeted recognition campaigns (e.g., highlighting specific donor groups in marketing materials or events). By combining engagement level with pattern-based filtering, managers can better tailor communication strategies and strengthen relationships with key donor segments.

## Database Information

Name of the database: al_Group_21482_G3

Additional information: Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL TP_Q1();
