# MIST4610-Project-2

Team Members:

Jake Rubenstein | Jacob.Rubenstein@uga.edu | [jakerubenstein27](https://github.com/jakerubenstein27)

Kaveri Channappa | Kaveri.Channappa@uga.edu | [kaverichannappa](https://github.com/kaverichannappa)

Gus Novak | jan82663@uga.edu | [GusNovak22](https://github.com/GusNovak22)

Caden Floyd | cadenfloyd7@uga.edu | [cflo-7](https://github.com/cflo-7)

<img width="963" height="676" alt="Screenshot 2025-11-29 at 8 41 18 PM" src="https://github.com/user-attachments/assets/9d49e69d-53ee-4124-a417-ed19f4cb89ed" />

Data Model Explanation: 

This database models the core operational aspects of Jackson Hole Airport which serves as the primary commercial airport for Jackson, Wyoming and the surrounding Teton County region. Despite being a smaller airport, it plays a critical role in supporting both tourism and local transportation, particularly due to its proximity to Grand Teton National Park and Jackson Hole Mountain Resort. 

The Airport table represents each airport in the system, including Jackson Hole, Denver, Salt Lake City, and Dallas Fort-Worth. Each airport has a unique identifier and includes attributes such as a AirportName, City, State, and Country.

The Gates table models all arrival and departure gates at each airport. Each gate has a unique identifier, name, and current operational status. The one to many relationship between Airports and Gates allows each Airport to have many functioning gates. 

The Flights table represents individual scheduled flights over a defined time period. Each flight includes attributes such as a unique flight ID, departure time, arrival time, date, and status. Flights are connected to two Gates (one for departure and one for arrival) and two Airport entities (departure and arrival), forming multiple one to many relationships. Additionally, each Flight is associated with one Airline and one Aircraft. 

The Airlines table represents major carriers servicing Jackson Hole Airport, including United, Delta, American, Alaska, and Sun Country Airlines. Each airline operates multiple Flights and utilizes various Aircraft models. The Aircraft table stores the specific planes used by these airlines, including model, year, range, and passenger capacity.

Passengers traveling through the airport are stored in the Passengers table, which includes personal information such as name, date of birth, and home country. Because Passengers may take multiple Flights and each Flight carries many passengers, this relationship is modeled using an associative entity that also stores Flight specific passenger details such as boarding priority. 

The Baggage table tracks all checked and carry on luggage associated with passengers. Since Baggage can travel on multiple connecting Flights, and each flight carries many bags, their relationship is modeled using another associative entity that records which baggage is on which flight as well as the bag weight for that specific flight. 

The AirportEmp table stores airport staff such as TSA officers, ground crew, gate agents, and maintenance workers. Each Employee is assigned to a single Airport, forming a one to many relationship between Airports and Employees. The AirportEmp table tracks the information of all employees at the airports. It maintains a unique identifier for each employee and tracks data such as first and last name and department the employee works for. This entity maintains a one to one recursive relationship with itself to account for the relationship of some employees as others' boss. 

<img width="649" height="633" alt="Screenshot 2025-11-29 at 8 34 36 PM" src="https://github.com/user-attachments/assets/06e54785-8e3c-46ae-8840-600db705d84a" />
<img width="646" height="630" alt="Screenshot 2025-11-29 at 8 35 03 PM" src="https://github.com/user-attachments/assets/ed753473-6c38-4502-ad39-38aa06b7d331" />
<img width="644" height="602" alt="Screenshot 2025-11-29 at 8 35 27 PM" src="https://github.com/user-attachments/assets/b6d447ca-8b6f-4c9b-920d-3eff9ead9bc0" />
<img width="645" height="651" alt="Screenshot 2025-11-29 at 8 35 50 PM" src="https://github.com/user-attachments/assets/205e3568-d94a-429b-80ab-8520a3f88295" />
<img width="644" height="623" alt="Screenshot 2025-11-29 at 8 36 12 PM" src="https://github.com/user-attachments/assets/106e5aa0-0516-4f71-8f7f-036f68514c79" />
<img width="640" height="229" alt="Screenshot 2025-11-29 at 8 36 59 PM" src="https://github.com/user-attachments/assets/02a66888-2c9d-48d3-9ee5-fba40abff922" />

Data Visualizations:

<img width="1201" height="685" alt="image" src="https://github.com/user-attachments/assets/68fc3bb9-a41c-4ac2-90d3-56cfdd5dfa9f" />

Executive Summary of Dashboard: 
This dashboard provides a comprehensive operational overview of flight activity, workforce distribution, and airline performance at Jackson Hole Airport. By integrating flight records, employee data, and airline schedules, the dashboard delivers insights into the airport's operational efficiency during the early January travel period, one of the busiest months for Jackson Hole due to winter tourism. The visualizations highlight three critical areas: flight reliability, daily traffic patterns, and resource allocation. 

Status of Flights: This visual shows the distribution of flights that were on time, delayed, or cancelled. For Jackson Hole airport, this metric is especially important because the airport is located in a mountainous region where weather conditions, such as snow, fog, and winter storms, can significantly disrupt flight operations. Monitoring the proportion of delayed or cancelled flights helps airport management identify operational challenges and determine whether issues stem from weather patterns, airline performance, or ground handling constraints. A high 'on-time' rate is vital for maintaining passenger satisfaction, especially given that Jackson Hole is heavily dependent on tourism during the winter ski season. 

Number of Flights Departing in January: This chart highlights the number of flights departing each day in early January, a critical time for Jackson Hole due to high tourism. Understanding daily flight volume helps the airport anticipate operational demand such as gate usage, runway scheduling, staffing levels, baggage handling and more. Variations in flight counts across the month can indicate tourist patterns, weather events, or scheduling adjustments. Tracking departures allows airport management to optimize travel resources during a busy season, such as January.

Count of Employees by Department: This visual presents the number of employees working across key airport departments such as Operations, Security, Baggage, Customer Service, Maintenance, and Administration. For Jackson Hole Airport, analyzing employee allocation is crucial for ensuring smooth daily operations, especially during peak travel periods. Departments like Operations and Security often carry heavier workloads due to safety regulations and the airport's unique geographic challenges. By understanding staffing distribution, management can assess whether the workforce is balanced appropriately and plan for future hiring to meet operational needs.

Number of Flights by Airline: This chart illustrates how many flights each airline operates at Jackson Hole Airport. Since JAC is a smaller regional airport served by a limited number of major carriers, such as Alaska Airlines, American Airlines, Delta, Sun Country, and United, understanding each airline's contribution to overall traffic is essential. This information helps the airport evaluate airline partnerships, route performance, and scheduling efficiency. It also supports capacity planning, negotiation of future routes, and ensuring that gate and ground operations meet the needs of the airlines with the highest traffic volumes. For an airport reliant on seasonal tourism, knowing which carriers drive the most passenger traffic informs planning and strategic growth decisions. 

Query #1: What are the full names and arrival destination of passengers who have checked baggage?

    SELECT CONCAT(FName, ' ',LName) AS PassengerName, City, StateAbbreviation, Airport.Country FROM Passengers 
    JOIN Passengers_has_Flight ON Passengers.PassengerID = Passengers_has_Flight.PassengerID
    JOIN Flight ON Passengers_has_Flight.FlightNumber = Flight.FlightNumber
    JOIN Airport ON Flight.ArrivalAirportID = Airport.AirportID
    WHERE EXISTS (SELECT * FROM Baggage WHERE Passengers.PassengerID = Baggage.Passengers_PassengerID AND Type = "Checked")
    ORDER BY FlightNumber DESC;

  This query first pulls the first and last names from the Passengers table and presents them together to show their PassengerName. The query then joins the Passengers_has_Flight table using the PassengerID data, the Flight table is then joined using PassengerID as well. The Airport entity is then joined using the ID of the airport the passengers are arriving at. This allows us to pull the location details from the Airport entity. The EXISTS statement includes passengers who have "Checked" baggage type in the Baggage table by joining the two tables on PassengerID. The data is then put in descending order in order to keep the flights grouped together. This information is useful to management because they determine "vacation" destinations and assign more resources and staff to these flights to account for more checked baggage. Management can also track down Passengers who have unclaimed luggage.

Query #2: Which gates at Denver International Airport have more than three passengers pass through and how many total?

    SELECT GateNumber, GateName, COUNT(PassengerID) as #ofPassengers from Passengers_has_Flight
    JOIN Flight ON Passengers_has_Flight.FlightNumber = Flight.FlightNumber
    JOIN Gate ON Flight.DepartureGateID = Gate.GateID
    JOIN Airport ON Gate.AirportID = Airport.AirportID
    WHERE City REGEXP "Denver"
    GROUP BY GateNumber
    HAVING #ofPassengers > 3;

   This query pulls Gate details and the count of passengers for these gates. The query first joins the Passengers_has_Flight table and Flight table using FlightNumber. The Gate table is then joined using the ID of the departing gates. Finally, the Airport table is joined using AirportID. Once all these tables are pulled, we apply the contraint that the name of the Airport must include the word "Denver" using the REGEXP command. We then group the data by GateNumber in order to seperate the output into the desired format where each individual Gate has a seperate count of passengers. The HAVING clause guarentees that we are only shown the gates that have more than three passengers passing through. This data is valuable for Denver International Airport because if they decide to add on resturants and stores to certain gates, they can know which ones are passed through more.

Query #3: Who are the Managers of the maintence department at each airport and how many subordinates do they have?

    SELECT AirportName, Boss.AirportEmpID, CONCAT(Boss.FNAME, ' ', Boss.LNAME) as DeptHeadName, COUNT(Emp.AirportEmpID) as SubordinateCount 
    FROM AirportEmp Boss 
    JOIN AirportEmp Emp ON Boss.AirportEmpID = Emp.AirportEmpManagerID
    JOIN Airport ON Boss.AirportID = Airport.AirportID
    WHERE Boss.Department = "Maintenance"
    GROUP BY Boss.AirportEmpID;

   This query pulls the full name of maintenance bosses at all airports and give the amount of employees they supervise. The query first performs a recursive join of the AirportEmp table creating a Boss and Emp copy. These tables are joined by The Boss table's AirportEmpID and the Emp table's AirportEmpManagerID. The Emp value represents who they report to which matches to another employee in the boss table. The Airport table is then joined so that the AirportName each manager works at can be pulled. The WHERE clause then adds a constraint in which we only pull managers of "Maintenance" departments. The GROUP BY clause ensures that the aggregated count function is grouped by the boss of each airport. This data would be useful for airport management to ensure proper supervision of subordinates and discipline for failure to meet maintenance standards.
