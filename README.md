# Supply_chain_logistics

## Problem Statement:
In modern supply chain logistics, carbon emissions generated from transportation and storage activities contribute significantly to environmental degradation. With increasing global pressure to reduce carbon footprints, logistics companies must identify actionable strategies to minimize emissions without compromising efficiency or cost-effectiveness.

This project aims to develop a deep learning model that accurately predicts carbon emissions based on key operational features such as transportation distance, cargo weight, warehouse capacity, and storage cost. By leveraging historical logistics data and integrating predictive analytics, the model enables stakeholders to estimate the environmental impact of different logistics decisions.

Additionally, the project provides a route suggestion mechanism that estimates emissions for new shipment scenarios, supporting more sustainable planning. The ultimate goal is to optimize logistics operations in a way that balances cost, efficiency, and environmental responsibility.

## Dataset Description

Dataset is divided into 7 tables, one table for all orders that needs to be assigned a route – OrderList table, and 6 additional files specifying the problem and restrictions. For instance, the FreightRates table describes all available couriers, the weight gaps for each individual lane and rates associated. The PlantPorts table describes the allowed links between the warehouses and shipping ports in real world. Furthermore, the ProductsPerPlant table lists all supported warehouse-product combinations. The VmiCustomers lists all special cases, where warehouse is only allowed to support specific customer, while any other non-listed warehouse can supply any customer. Moreover, the WhCapacities lists warehouse capacities measured in number of orders per day and the WhCosts specifies the cost associated in storing the products in given warehouse measured in dollars per unit.

Order ID is ID of the order made by the customer, product ID is the specific product ID customer ordered.

"tpt_day_cnt" in the FrieghtRates table means transportation day count, i.e. estimated shipping time.

WhCapacities correspond to the number of orders. For example, let's say Customer 1 requests 10 units of X, Customer 2 requests 20 units of Y. The total number of orders is 2, thus total capacity in "whCapacity" is 2.

WhCapacities table is the maximum number of orders that can be processed per each plant, it is not dependant on specific products.

The OrderList contains historical records of how the orders were routed and demand satisfied. The whCapacities and rest of the tables are the current state constraints of the network. Thus, we can calculate the costs of historical network and also optimize for the new constraints.

In order to build Linear Programming (LP) model, you would take the following from the OrderList: the product ID that needs to be shipped, the destination port, unit quantity (for cost) and unit weight (for weight constraints). And then use the limits of those constraints from other tables.

Questions: There is a Carrier V44_3 in OrderList table, but it is missing in the FreightRates table? V44_3 is a carrier that was historically used for supplying given demand, but since it has been discontinued and therefore do not appear in the Freight Rates List. Also, all of the V44_3 instances are CRF - i.e. customer arranges their own shipping and hence cost is not calculated either way.
