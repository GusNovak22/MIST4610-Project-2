# MIST4610-Project-2

Data Model Explanation: 

This database models the core operational aspects of Jackson Hole Airport which serves as the primary commercial airport for Jackson, Wyoming and the surrounding Teton County region. Despite being a smaller airport, it plays a critical role in supporting both tourism and local transportation, particularly due to its proximity to Grand Teton National Park and Jackson Hole Mountain Resort. 

The Airport table represents each airport in the system, including Jackson Hole, Denver, Salt Lake City, and Dallas Fort-Worth. Each airport has a unique identifier and includes attributes such as a name, city, and state.

The Gates table models all arrival and departure gates at each airport. Each gate has a unique identifier, name, and current operational status. The one to many relationship between Airports and Gates allows each Airport to have many functioning gates. 

The Flights table represents individual scheduled flights over a defined time period. Each flight includes attributes such as a unique flight ID, departure time, arrival time, date, and status. Flights are connected to two Gates (one for departure and one for arrival) and two Airport entities (departure and arrival), forming multiple one to many relationships. Additionally, each Flight is associated with one Airline and one Aircraft. 
The Airlines table represents major carriers servicing Jackson Hole Airport, including United, Delta, American, Alaska, and Sun Country Airlines. Each airline operates multiple Flights and utilizes various Aircraft models. The Aircraft table stores the specific planes used by these airlines, including model and passenger capacity.
Passengers traveling through the airport are stored in the Passengers table, which includes personal information such as name, date of birth, and home country. Because Passengers may take multiple Flights and each Flight carries many passengers, this relationship is modeled using an associative entity that also stores Flight specific passenger details such as boarding priority. 
The Baggage table tracks all checked and carry on luggage associated with passengers. Since Baggage can travel on multiple connecting Flights, and each flight carries many bags, their relationship is modeled using another associative entity that records which baggage is on which flight as well as the bag weight for that specific flight. 
The Employees table stores airport staff such as TSA officers, ground crew, gate agents, and maintenance workers. Each Employee is assigned to a single Airport, forming a one to many relationship between Airports and Employees. 

<img width="652" height="813" alt="Screenshot 2025-11-26 at 3 52 42 PM" src="https://github.com/user-attachments/assets/15e5a2ba-a2a8-409e-a0e9-ac246eb658b7" />
<img width="649" height="833" alt="Screenshot 2025-11-26 at 3 52 57 PM" src="https://github.com/user-attachments/assets/0a3fab7f-565f-4ea0-bbf1-d37bc90e7d94" />
<img width="665" height="583" alt="Screenshot 2025-11-26 at 3 53 08 PM" src="https://github.com/user-attachments/assets/eb46bded-4ca4-412b-ae9d-a664a9fc336d" />
<img width="648" height="821" alt="Screenshot 2025-11-26 at 3 53 21 PM" src="https://github.com/user-attachments/assets/698eeabd-5e14-438b-b506-67faa1e845f1" />


