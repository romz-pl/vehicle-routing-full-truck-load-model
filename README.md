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


### Legal Regulations

+ **[Drivers' labor law](https://en.wikipedia.org/wiki/Drivers%27_working_hours)**: The model must account for legal regulations governing drivers' working hours, which is crucial for ensuring driver safety and well-being.
+ **[Cabotage transport](https://en.wikipedia.org/wiki/Cabotage)**: Regulations concerning cabotage transport must be incorporated into the model.

These drivers' labor law and cabotage transport regulations are primary sources of the model's complexity.
First, drivers' working hours directly influence travel time between two points on a map. 
Therefore, to calculate the travel time of a route, the current status of the driver's activity must be considered. 
As a result, the directed graph under consideration is not static; rather, some arcs are dynamic in the sense that they depend on the specific route being examined. 
For example, the required travel distance may be short; however, the driver may not be permitted to drive and must wait until a mandatory break period ends.

Additionally, regulations regarding drivers' working hours provide an added level of flexibility. 
A careful reading of these regulations reveals that drivers have some discretion in deciding when to take breaks. 
With this flexibility, travel time between two points on the map depends on the driver's decisions. 
However, drivers must take breaks in parking spaces designated for trucks. 
Since such safe parking locations are scarce, drivers' working time is correlated with parking space availability. 
Incorporating this correlation into the model could provide business value, as it would enable opportunities to reserve parking spaces in advance.


### Business Strategy

The goal of every business strategy is to create value. 
In the context of the vehicle routing problem, this value is represented by an optimal work schedule that determines which driver will fulfill which orders. 
However, since numerous business strategies exist, there are correspondingly many approaches to generating an effective work schedule. 
Therefore, designing a flexible mathematical model that encompasses the broad spectrum of possible business strategies is essential.

The business strategy for the vehicle routing problem depends heavily on both the **time horizon** and the **geographic area** of operations. 
For example, consider a company that delivers goods within Poland, where each driver returns to the base daily. 
In contrast, another company might operate throughout Europe, with drivers returning to the base weekly or biweekly. 
Both scenarios are realistic and raise a critical business question: **"What is the optimal schedule for the company?"**.
The answer to this question is fundamental to developing the appropriate mathematical model and, consequently, the proper software implementation. 

To illustrate this, consider the following business case: 
A company operates throughout Europe and requires its drivers to return to the base every Friday. 
Given this one-week planning horizon, it is reasonable to assume that new orders will emerge while drivers are already en route. 
This raises a strategic dilemma: Should the business provide each driver with a complete list of orders for the entire five-day period, 
or would it be more optimal to assign only the next order? 
Perhaps assigning the next two orders to each driver represents an even more effective strategy.

Once these questions have been formulated, it becomes evident that the schedule and the construction of the order portfolio are closely interrelated. 
Specifically, if the order portfolio is fixed, the schedule can be determined in advance. 
However, when orders are dynamically added to or removed from the portfolio, the optimal strategy becomes unclear.
The most complex situation arises when the company actively influences which orders are added to or removed from the portfolio. 
In such cases, the company can be characterized as an order trading entity, as buying and selling orders directly affects the portfolio's structure. 
This creates a strong interdependence between order portfolio construction and driver schedule generation, requiring a mathematical model that can accommodate this dynamic relationship.



### Order Portfolio
Every transport company maintains an order portfolio. In the most general case, the structure of this portfolio is highly dynamic. 
The portfolio manager has the authority to buy and sell orders. 
However, contractual agreements with customers dictate that certain orders cannot be sold and must be fulfilled by the company.
Furthermore, the portfolio manager faces the complex task of determining which orders to acquire and which to divest. 
This gives rise to a critical business question: **"What constitutes the optimal portfolio for the company?"**.
This overarching question can be decomposed into more specific inquiries related to the **value** and **stability** of the portfolio.

The value of the portfolio determines the revenue generated from order fulfillment. 
However, since only the schedule is guaranteed, the revenue is not fixed. 
If the schedule cannot be completed, the revenue could be significantly reduced. 
A schedule may be disrupted for numerous reasons, including driver illness, vehicle breakdowns, traffic congestion, adverse weather conditions, and road accidents.
Given these contingencies, it is essential to construct a portfolio that remains viable even when disruptions occur. 
A portfolio capable of withstanding such circumstances is considered stable.

As previously mentioned, mathematical models should incorporate the key features of an order portfolio, such as value, revenue potential, and stability. 
Consequently, systems built upon these models must support the decision-making processes of portfolio managers. 
Specifically, users should be able to evaluate the value of prospective orders and assess their impact on the portfolio's overall value and stability. 
Ideally, the system would autonomously facilitate order selection. 
Given a set of available orders, the system should recommend which orders to acquire and which to divest.


### Implementation

This section provides an overview of the IT system characteristics derived from the mathematical model. 
It is important to note that a substantial portion of the model addresses optimization problems, including portfolio and schedule optimization. 
These problems belong to the class of combinatorial optimization and exhibit nonlinearity due to driver labor law constraints.

The solution approach for these problems remains an open question, though approximation algorithms based on metaheuristics, 
such as [GRASP](https://en.wikipedia.org/wiki/Greedy_randomized_adaptive_search_procedure) (Greedy Randomized Adaptive Search Procedures), appear to be the most viable option.

System implementers must recognize that this is a **real-time decision support system** required to process millions of orders and coordinate thousands of trucks. 
Given the system's scale and the need for real-time decision-making capabilities, the architecture must be designed from the ground up for deployment on a distributed computing cluster.
Performance requirements demand serious attention, necessitating extensive scalability testing to ensure the system maintains smooth operation under diverse load patterns. 
Additionally, the system must support customization to accommodate the varying needs of different companies. 
Such customization encompasses the distinct business strategies of different transportation companies, as well as the ability for individual companies to adapt their strategies dynamically over time.



### Summary

This document presents the structure of a mathematical model developed for a full truckload shipping company. 
While the model itself represents a valuable contribution, the document's most significant value lies in its comprehensive business analysis of the transportation company's critical operational aspects.

A key emphasis throughout this work is the importance of building a system that extends beyond the 
mathematical model itself — one that encompasses and supports multiple business activities in an integrated manner. 
Of particular note is the **strong correlation identified between portfolio management decisions and schedule construction**, 
highlighting the interconnected nature of these strategic choices.

The proposed mathematical model employs directed graphs as its foundational framework, which constitutes one of its distinguishing technical features. 
However, the document's primary contribution remains its thorough examination of the business problems inherent to full truckload operations,
providing context and practical relevance to the mathematical formulation.



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
