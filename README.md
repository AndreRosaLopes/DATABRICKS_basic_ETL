# Databricks – Basic Retail Project

The goal of this project is to explore and evaluate key Databricks features through a retail sales use case.

---

## Requirements (High Level)

![Requirements Diagram](excalidraw/requirements.png)

1. **Daily Batch Input**  
   We will receive daily batches of JSON files (generated in Python) in the following formats:
   - `YYYY-MM-DD_Customer.json`
   - `YYYY-MM-DD_Products.json`
   - `YYYY-MM-DD_Sales.json`

2. **Date Control**  
   We need fine-grained control over the processing dates according to the operational source system.  
   For example: *Up to which date has the data mart (or table itself) been updated?*

---

## Design Process

### 1. Select the Business Process to Model
The business process chosen for this case study is **retail sales**.  
The dataset will allow us to analyze:
- Which products are sold
- In what quantity
- To which customers
- At what price
- On which date and time

### 2. Define the Grain
We define the grain as **a single product sold**, representing the most granular data available from the operational system.

### 3. Choose the Dimensions
The descriptive dimensions for this model are:
- **Product**
- **Customer**
- **Date**

### 4. Identify the Facts
The fact table will represent **individual sales items**.

---

## First Solution: [*pure SQL notebooks*](First_solution.md)

The objectives are:

- Define tables and views to control data movement dates  
- Create `tasks` to manage date-based loads  
- Explore the use of `COPY INTO` (considered a legacy approach compared to Auto Loader for pure SQL solutions)  
- Define **quarantine tables** and a mechanism to re-ingest quarantined data  
- Use Databricks **Workflows** to orchestrate tasks (via notebooks)  
  - The approach is to have one job per project, establishing dependencies and using ```FOR EACH``` to process tasks incrementally — one day at a time — whenever possible.
  - Develop the job directly from the YAML file rather than the UI — this approach is faster, easier to maintain, and offers a clearer overall view of the job structure.
- Leverage the following tools for development:
  - **Databricks Asset Bundles**
  - **Databricks Connect**
  - **GitHub**
  - **VS Code**

---


