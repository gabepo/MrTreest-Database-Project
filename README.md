
# MIST 4610 Group Project 1: Mr. Treest

## Team Name - 21482 Group 3

Team Members:
- Tyson Elmore [@TysonElmore](https://github.com/TysonElmore)
- Matthew Liu [@marshy6](https://github.com/marshy6)
- Lucas Luxemburger [@lucasjbluxemburger](https://github.com/lucasjbluxemburger)
- Gabe Po [@gabepo](https://github.com/gabepo)
- Chris Trinh [@cat35795](https://github.com/cat35795)

## Scenario Description

The Mr. Treest Tree Planting Non-Profit Organization (MTTPNPO) uses an advanced, data-integrated strategy that connects environmental impact and financial oversight to further its goals of urban reforestation and community involvement. To ensure transparent reporting, this ecosystem starts with donors whose contributions are closely monitored and frequently limited to programs. These initiatives are carried out through individual planting ceremonies at predetermined locations. The organization uses a hierarchical geographic lens to monitor impact, dividing beneficiary groups into subcommunities through recursive relationships. This allows for fine grained tracking from the city to level down to individual neighborhoods. A recursive tree replacement connection guarantees a longitudinal history of canopy health, and each tree is recorded by its species to track scientific data such as growth rates. Underpinning these operations is a robust human resource framework where volunteers all of whom undergo a volunteer background check for public safety compliance are managed via a volunteer assignment entity that records their specific volunteer role and hours worked. By synthesizing these financial, geographic, botanical, and human resource pillars into a single database, MTTPNPO provides a comprehensive, transparent view of how donor funds are transformed into thriving urban forests through community-led action. 

 
## Data Model

(Below is a chatGPT'd data model explanation that can be rewritten to sound more human)

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

Overall, this model supports tracking financial contributions, program execution, volunteer involvement, and community impact in a structured and relational way.

<img width="856" height="749" alt="image" src="https://github.com/user-attachments/assets/adb2615b-b50f-402f-9091-c5b9a167c91c" />

## Data Dictionary

...

## Queries

(insert screenshot of query information table)

### Query 1: Total donations by program 
(description)

(screenshot of code goes here)

(justification)

### Query 2: ... 
(description)

(screenshot of code goes here)

(justification)

(repeat above for the rest)

## Database Information

hi
