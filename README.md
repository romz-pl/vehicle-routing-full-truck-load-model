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


## Mathematical model based on directed graph

The Full Truck Load (FTL) model uses a directed graph $G = (N, A)$ to represent the transportation network as a set of nodes $N$, 
which represent locations such as origins, destinations, and hubs, and a set of directed arcs $A$, 
which represent permitted travel routes, empty repositioning, and waiting actions. This framework allows for the modeling of complex, 
asymmetric, and time-dependent constraints often present in FTL operations, such as driver hours of service, time windows, and vehicle capacity.


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
