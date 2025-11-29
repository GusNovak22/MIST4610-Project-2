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


Data Visualizations:

<img width="1201" height="685" alt="image" src="https://github.com/user-attachments/assets/68fc3bb9-a41c-4ac2-90d3-56cfdd5dfa9f" />

Executive Summary of Dashboard: 
This dashboard provides a comprehensive operational overview of flight activity, workforce distribution, and airline performance at Jackson Hole Airport. By integrating flight records, employee data, and airline schedules, the dashboard delivers insights into the airport's operational efficiency during the early January travel period, one of the busiest months for Jackson Hole due to winter tourism. The visualizations highlight three critical areas: flight reliability, daily traffic patterns, and resource allocation. 

Status of Flights: This visual shows the distribution of flights that were on time, delayed, or cancelled. For Jackson Hole airport, this metric is especially important because the airport is located in a mountainous region where weather conditions, such as snow, fog, and winter storms, can significantly disrupt flight operations. Monitoring the proportion of delayed or cancelled flights helps airport management identify operational challenges and determine whether issues stem from weather patterns, airline performance, or ground handling constraints. A high 'on-time' rate is vital for maintaining passenger satisfaction, especially given that Jackson Hole is heavily dependent on tourism during the winter ski season. 

Number of Flights Departing in January: This chart highlights the number of flights departing each day in early January, a critical time for Jackson Hole due to high tourism. Understanding daily flight volume helps the airport anticipate operational demand such as gate usage, runway scheduling, staffing levels, baggage handling and more. Variations in flight counts across the month can indicate tourist patterns, weather events, or scheduling adjustments. Tracking departures allows airport management to optimize travel resources during a busy season, such as January.

Count of Employees by Department: This visual presents the number of employees working across key airport departments such as Operations, Security, Baggage, Customer Service, Maintenance, and Administration. For Jackson Hole Airport, analyzing employee allocation is crucial for ensuring smooth daily operations, especially during peak travel periods. Departments like Operations and Security often carry heavier workloads due to safety regulations and the airport's unique geographic challenges. By understanding staffing distribution, management can assess whether the workforce is balanced appropriately and plan for future hiring to meet operational needs.

Number of Flights by Airline: This chart illustrates how many flights each airline operates at Jackson Hole Airport. Since JAC is a smaller regional airport served by a limited number of major carriers, such as Alaska Airlines, American Airlines, Delta, Sun Country, and United, understanding each airline's contribution to overall traffic is essential. This information helps the airport evaluate airline partnerships, route performance, and scheduling efficiency. It also supports capacity planning, negotiation of future routes, and ensuring that gate and ground operations meet the needs of the airlines with the highest traffic volumes. For an airport reliant on seasonal tourism, knowing which carriers drive the most passenger traffic informs planning and strategic growth decisions. 

Query #1: What are the full names and arrival destination of passengers who have checked baggage?
SELECT CONCAT(FName, ' ',LName) as PassengerName, City, StateAbbreviation, Airport.Country FROM Passengers
  JOIN Passengers_has_Flight ON Passengers.PassengerID = Passengers_has_Flight.PassengerID
  JOIN Flight ON Passengers_has_Flight.FlightNumber = Flight.FlightNumber
  JOIN Airport ON Flight.ArrivalAirportID = Airport.AirportID
  WHERE EXISTS (SELECT * FROM Baggage WHERE Passengers.PassengerID = Baggage.Passengers_PassengerID AND Type = "Checked")
  ORDER BY FlightNumber DESC;

This query first pulls the first and last names from the Passengers table and presents them together to show their PassengerName. The query then joins the Passengers_has_Flight table using the PassengerID data, the Flight table is then joined using PassengerID as well. The Airport entity is then joined using the ID of the airport the passengers are arriving at. The EXISTS statement includes passengers who have "Checked" baggage type in the Baggage table by joining the two tables on PassengerID. The data is then put in descending order in order to keep the flights grouped together. This information is useful to management because they determine "vacation" destinations and assign more resources and staff to these flights to account for more checked baggage. Management can also track down Passengers who have unclaimed luggage.

Query #2: 
