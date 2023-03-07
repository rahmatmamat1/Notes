## What is Data Modelling?

Data modeling is the process of creating a conceptual, logical, or physical representation of data, in order to facilitate the storage, processing, and analysis of that data. Data models can be used to define the structure, relationships, and constraints of data in a way that is understandable and useful to both humans and machines.

There are three main types of data models:
1. **Conceptual data models**: These models describe the high-level business concepts and relationships between them. They are often used in the early stages of a project to help stakeholders understand the scope and requirements of the data.
2. **Logical data models**: These models describe the data at a more detailed level, including the entities, attributes, and relationships between them. They are often used to design and implement databases or other data storage systems.
3. **Physical data models**: These models describe the actual structure of the data in a specific technology or platform. They include details such as data types, keys, indexes, and other physical constraints.

## How to develop data model?

Data modeling typically involves several steps, including:
1. **Requirements gathering**: This involves understanding the business requirements for the data, and defining the scope and objectives of the modeling effort.
2. **Conceptual modeling**: This involves creating a high-level conceptual model that captures the key business concepts and relationships.
3. **Logical modeling**: This involves creating a more detailed model that defines the entities, attributes, and relationships between them, often using a notation such as Entity-Relationship (ER) or Unified Modeling Language (UML).
4. **Physical modeling**: This involves defining the physical structure of the data, including data types, keys, indexes, and other physical constraints, often using a notation such as Data Definition Language (DDL) or schema diagrams.

Data modeling can be a complex process, but it is essential for ensuring that data is organized, structured, and managed in a way that supports effective analysis and decision-making. By creating clear and consistent data models, organizations can ensure that data is accurate, reliable, and easily accessible, and can avoid the risks and costs associated with poorly structured or inconsistent data.

## Kimball’s Dimensional Modeling

Kimball's Dimensional Modeling is a data modeling technique used in data warehousing and business intelligence projects. The objective of Kimball's Dimensional Modeling is to design a data model that is optimized for querying and analysis, and that can support the reporting and analysis needs of the business users.

The approach used in Kimball's Dimensional Modeling involves creating a set of dimension tables and fact tables. Dimension tables contain descriptive information about the business entities, such as customers, products, and time periods, and are organized hierarchically. Fact tables contain the quantitative measures or events that the business wants to analyze, such as sales, inventory levels, or website visits.

The key principles of Kimball's Dimensional Modeling include:
1. **Dimensional modeling is business-focused**: The data model should reflect the business processes and entities, and be designed with the needs of the business users in mind.
2. **Dimensions and facts are separate**: Dimension tables should contain descriptive attributes, such as names, addresses, and product descriptions, while fact tables should contain quantitative measures, such as quantities, amounts, and durations.
3. **Dimension tables are denormalized**: Dimension tables are typically denormalized, which means that they contain redundant attributes to enable faster querying and analysis.
4. **Fact tables are additive**: Fact tables contain quantitative measures that can be aggregated across different dimensions and levels of granularity.
5. **Conformed dimensions and facts**: Dimension and fact tables should be designed to be reusable across different data marts and business processes.

The benefits of Kimball's Dimensional Modeling approach include:
- **Improved query performance:** The denormalized dimension tables and additive fact tables enable fast querying and analysis of large data sets.
- **Improved usability**: The data model is designed with the needs of the business users in mind, and is optimized for reporting and analysis.
- **Flexibility**: The data model can be easily adapted to changing business requirements and new data sources.
- **Consistency**: The use of conformed dimensions and facts enables consistency across different data marts and business processes.

Overall, Kimball's Dimensional Modeling is a popular approach to data modeling in data warehousing and business intelligence projects, and is widely used in many industries and organizations.

## Element of Dimensional Modelling

Star schema is a type of database schema used in data warehousing and business intelligence projects. It is designed to be optimized for querying and reporting by organizing data into a set of dimension tables and a central fact table.

The fact table in a star schema contains the quantitative measures or events that the business wants to analyze, such as sales, inventory levels, or website visits. Each row in the fact table represents a specific event or measure and includes one or more foreign keys that reference the corresponding dimension tables. For example, a sales fact table might include a foreign key to a product dimension table and a customer dimension table, to enable analysis of sales by product and customer.

Dimension tables contain descriptive information about the business entities, such as customers, products, and time periods, and are organized hierarchically. Each row in a dimension table represents a specific entity, and includes one or more attributes that describe the entity. For example, a product dimension table might include attributes such as product name, product category, and product supplier, to enable analysis of sales by product category and supplier.

The fact table and dimension tables are joined together using foreign keys, which enable the aggregation and filtering of data across multiple dimensions. For example, a business might use a star schema to analyze sales by product, customer, and time period, enabling them to identify trends and patterns in sales over time.

-   _**Fact Table**_:
    -   _Facts_ = _Measures_
    -   Typically numeric values which can be aggregated, such as measurements or metrics.
        -   Examples: sales, orders, etc.
    -   Corresponds to a _business process_.
    -   Can be thought of as _"verbs"_.
-   _**Dimension Table**_:
    -   _Dimension_ = _Context_
    -   Groups of hierarchies and descriptors that define the facts.
        -   Example: customer, product, etc.
    -   Corresponds to a _business entity_.
    -   Can be thought of as _"nouns"_.

The benefits of using a star schema include:
* Improved query performance: The use of a central fact table and denormalized dimension tables enables faster querying and analysis of large data sets.
* Improved usability: The star schema is designed to be easy to understand and use by business users, enabling faster and more accurate decision-making.
* Flexibility: The star schema can be easily adapted to changing business requirements and new data sources.
* Scalability: The star schema can support large volumes of data and complex analysis.

Overall, the star schema is a popular and effective approach to organizing data for querying and reporting, and is widely used in many industries and organizations.

## Architecture of Dimensional Modelling

A good way to understand the _architecture_ of Dimensional Modeling is by drawing an analogy between dimensional modeling and a restaurant:

-   Stage Area:
    -   Contains the raw data.
    -   Not meant to be exposed to everyone.
    -   Similar to the food storage area in a restaurant.
-   Processing area:
    -   From raw data to data models.
    -   Focuses in efficiency and ensuring standards.
    -   Similar to the kitchen in a restaurant.
-   Presentation area:
    -   Final presentation of the data.
    -   Exposure to business stakeholder.
    -   Similar to the dining room in a restaurant.