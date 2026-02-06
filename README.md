# Full Truck Load Problem

> [!NOTE]
> The **vehicle routing problem (VRP)** is a combinatorial optimization and integer programming problem which asks
> "What is the optimal set of routes for a fleet of vehicles to traverse in order to deliver to a given set of customers?"
> The problem first appeared, as the truck dispatching problem, in a paper by George Dantzig and John Ramser in 1959,
> in which it was applied to petrol deliveries. Often, the context is that of delivering goods located at a central
> depot to customers who have placed orders for such goods. However, variants of the problem consider, e.g, collection
> of solid waste and the transport of the elderly and the sick to and from health-care facilities.
> The standard objective of the VRP is to minimise the total route cost. Other objectives, such as minimising
> the number of vehicles used or travelled distance are also considered.
>
> Wikipedia: [Vehicle routing problem](https://en.wikipedia.org/wiki/Vehicle_routing_problem)


> [!NOTE]
> **Full Truck Load (FTL) shipping** is freight transport in which a semi-trailer or intermodal container is filled entirely
> with one type of cargo. It differs from less-than-truckload shipping (LTL) in which freight from multiple
> customers is combined in one trailer. A truckload carrier is a trucking company that contracts entire trailer-load to a single customer.
>
> Wikipedia: [Truckload shipping](https://en.wikipedia.org/wiki/Truckload_shipping)


## Mathematical Model Based on Directed Graph

The Full Truck Load (FTL) model uses a directed graph $G = (N, A)$ to represent the transportation network as a set of nodes $N$, 
which represent locations such as origins, destinations, and hubs, and a set of directed arcs $A$, 
which represent permitted travel routes, empty repositioning, and waiting actions. This framework allows for the modeling of complex, 
asymmetric, and time-dependent constraints often present in FTL operations, such as driver hours of service, time windows, and vehicle capacity.

### Core Components of the Directed Graph 
+ **Nodes**, $N$: Represent geographic locations including pick-up points, delivery points, depots, and artificial source/sink nodes $N_{0}$, $N_{\infty}$ to represent the start and end of a vehicle's tour.
+ **Arcs**, $A$: Represent the paths between locations. In a directed graph, the arc $i \rightarrow j$ is distinct from $j\rightarrow i$, allowing for one-way roads or different travel times/costs in opposite directions.
+ **Weights**: Arcs are typically weighted with costs (distance, fuel, tolls) and travel times. 
+ **Arc Types**:
  + **Service Arcs**: Represent loaded, revenue-generating trips.
  + **Empty Travel Arcs**: Represent repositioning of empty trucks to the next pick-up point.
  + **Waiting Arcs**: Represent trucks waiting at a node to meet time window constraints.


### Key Features of FTL Modeling on Directed Graphs

+ **Time-Space Representation**: The graph often incorporates time as a dimension, creating a "time-expanded graph." In this type of graph, nodes are defined as $(location, time)$, enabling the modeling of time-dependent constraints such as delivery windows.
+ **Full Truck Load Constraint**: Since each truck is loaded to capacity, the model typically involves pairing a specific pickup node with a specific delivery node and treating it as direct service.
+ **Objective Function**: The goal is usually to reduce total costs, which includes operating costs (distance-based) and waiting/empty travel costs.
+ **Solution Approach**: These problems are often NP-hard and are solved using metaheuristics to manage large-scale networks. The focus is on generating efficient routes and assigning trucks.


### Example Applications
+ **Dynamic FTL Routing**: This is used to solve problems where orders arrive in real time. It allows for the dynamic re-routing of vehicles based on current graph states.
+ **Pattern-Based Formulation**: This is used for multi-shift FTL scenarios and utilizes graph structures to generate feasible, cost-effective routes.
+ **Data-Driven Transport Mapping**: This method is applied to analyze freight movement in specific areas, such as the Port of Hamburg, in order to predict traffic volume and optimize routing.


### Legal regulations
+ **Drivers' labor law**: The model must take into account legal regulations concerning drivers' working hours, which is crucial for ensuring the safety and well-being of drivers.
+ **Cabotage transport**: Regulations concerning [cabotage transport](https://en.wikipedia.org/wiki/Cabotage) must be taken into account in the model.

These drivers' labor law regulations and cabotage transport regulations are the source of the model's complexity. 
First of all, the working hours of drivers directly influence travel time between two points on a map.
Therefore, in order to calculate the travel time of the track, the current status of the driver's activity must be taken into account.
As a result, the considered directed graph is not static, but some arcs are non-static in the sense that they depend on the considered track.
For example, the required distance to travel may be short; however, the driver is not allowed to drive. He or she must wait until the obligatory break ends.

Additionally, the regulations regarding drivers' work hours offer an added level of flexibility.
After careful reading of these regulations, it is clear that the driver has some flexibility in deciding when to take a break.
With this flexibility, the travel time between two points on the map depends on the driver's decisions.

However, the driver must take the brake in the parking space dedicated to the track.
Since such safe places are scarce, drivers' working time is correlated with the availability of parking spaces.
Considering this correlation could provide business value since it would allow for the opportunity to reserve a parking space.


### Business strategy

The goal of every business strategy is to create value. In the context of the vehicle routing problem, value is represented by an optimal work schedule.
This schedule determines which driver will take which orders. However, since there are many business strategies, there are also many ways to generate a work schedule. 
Therefore, designing a flexible mathematical model that encompasses the broad spectrum of possible business strategies is crucial.

The business strategy for the vehicle routing problem depends heavily on the time horizon and geographic area. 
For example, consider a company that delivers goods within Poland, where each driver returns to the base every day. 
Another example is a company that operates throughout Europe, where drivers return to the base every Friday or every other week. 
Both examples are realistic. With these two examples, the business question is: **"What is the optimal schedule for the company?"**.
The answer to this question is critical to providing the right mathematical model, and consequently, the proper software implementation.

More specifically, consider the following business case: A company operates throughout Europe and requires its drivers to return to the base every Friday.
For the one-week horizon, it is reasonable to assume that new orders will appear while the driver is on the route. 
With this in mind, what strategy should the business choose? 
Should it provide the complete list of orders for each driver for the next five days, or is it more optimal to provide only the next order?
Or perhaps the subsequent two orders for any driver in the company are even more optimal?

Once the questions have been determined, it becomes evident that the schedule and the construction of the order portfolio are closely related.
In other words, if the order portfolio is fixed, the schedule can be made in advance.
However, when orders are added to or deleted from the portfolio, it is unclear which strategy to choose.
The most complex situation occurs when the company influences which orders are added to or deleted from the portfolio.
In this case, the company can be considered a trading order company because buying and selling orders directly affects the portfolio's structure.
Therefore, there is a strong correlation between constructing the order portfolio and creating the schedule for drivers.


### Order portfolio

Every transport company has an order portfolio. In the most general case, the structure of this portfolio is highly dynamic.
The portfolio manager can buy and sell orders. 
However, due to agreements with customers, some orders cannot be sold and must be processed by the company.
Furthermore, the portfolio manager faces the complex task of deciding which orders to buy and which to sell.
Thus, the business question arises: **"What is the optimal portfolio for the company?"**
This general question can be broken down into more specific questions related to the value and stability of the portfolio.

The value of the portfolio determines the yield obtained from order processing. 
However, since only the schedule is guaranteed, the yield is not fixed.
If the schedule cannot be completed, the yield could be significantly smaller.
A schedule could be interrupted for many reasons, such as driver illness, broken trucks, traffic jams, terrible weather conditions, and accidents on the road.
Given these possibilities, it is necessary to create a portfolio that can be fulfilled even if an interruption occurs.
A portfolio that can withstand such circumstances is considered stable.



## References

### 2023
+ The Evolution of the Vehicle Routing Problem: A Survey of VRP Research and Practice from 2005 to 2022, [Chapter in: The Evolution of the Vehicle Routing Problem](https://doi.org/10.1007/978-3-031-18716-2_1)


### 2020
+ Green Transportation and New Advances in Vehicle Routing Problems, [Book](https://doi.org/10.1007/978-3-030-45312-1)


### 2019
+ Orienteering Problems: Models and Algorithms for Vehicle Routing Problems with Profits, [Book](https://doi.org/10.1007/978-3-030-29746-6)
+ Smart Delivery Systems: Solving Complex Vehicle Routing Problems, [Book](https://doi.org/10.1016/C2017-0-03660-1)


### 2017
+ Approximate Dynamic Programming for Dynamic Vehicle Routing, [Book](https://doi.org/10.1007/978-3-319-55511-9)


### 2016
+ Metaheuristics for Vehicle Routing Problems, [Book](https://doi.org/10.1002/9781119136767)


### 2015
+ Arc Routing: Problems, Methods, and Applications, [Book](https://doi.org/10.1137/1.9781611973679)
+ Operational Transportation Planning of Modern Freight Forwarding Companies: Vehicle Routing under Consideration of Subcontracting and Request Exchange, [Book](https://doi.org/10.1007/978-3-658-06869-1)


### 2014
+ Vehicle Routing: Problems, Methods, and Applications, [Book, 2nd Edition](https://doi.org/10.1137/1.9781611973594)


### 2008
+ The Vehicle Routing Problem: Latest Advances and New Challenges, [Book](https://doi.org/10.1007/978-0-387-77778-8)


### 2002
+ Vehicle Routing: Problems, Methods, and Applications, [Book, 1st Edition](https://doi.org/10.1137/1.9780898718515)


### 1988
+ Survey Paper - Time Window Constrained Routing and Scheduling Problems, [Transportation Science](https://doi.org/10.1287/trsc.22.1.1)


### 1964
+ Scheduling of Vehicles from a Central Depot to a Number of Delivery Points, [Operations Research](http://dx.doi.org/10.1287/opre.12.4.568)


### 1959
+ The Truck Dispatching Problem, [Management Science](https://www.jstor.org/stable/2627477)
