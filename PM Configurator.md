# PM Configurator Overview

The PM Configurator is a tool designed to automate and streamline the process of creating and managing Preventive Maintenance (PM) configurations within the Maximo system. It allows users to define the rules that govern how PMs should be created and managed. This document provides an overview of the key functionalities and processes involved in using the PM Configurator.

## Key Functionalities

### 1. Creating a New PM Configuration
Users can create a new PM configuration by entering values for the following fields:

- **PM Type**: Select from available PM types such as Telecom PM, Cooling PM, Power PM, or Baseload Genset PM.
- **Location Hierarchy Level**: Choose between EXCHANGE/BUILDING or MOBILE ACCESS.
- **WO Structure**: Select the work order structure from options like MULTIPLE WO ONE TASK, ONE WO MULTIPLE TASK, or ONE WO ONE TASK.
- **Section and Sub-section**: Select the relevant section and sub-section within the organization.
- **Frequency Type**: Choose between Fixed or Dynamic frequency types.
- **Classification**: Associate one or more classifications applicable for PM generation.
- **Task Name**: Choose the task name for each classification.

### 2. Dynamic Frequency Configuration
If the Frequency Type is selected as Dynamic, users can configure the frequency based on various parameters:

- **Frequency Parameters**: Select from a list of 12 parameters and assign a weightage percentage to each.
- **Parameter Values**: Define the value types for each parameter and their corresponding weightage percentages.
- **Frequency Range**: Define the frequency range and cycle according to which work orders are generated automatically.

### 3. Updating Existing Configurations
Users can update existing PM configurations in several ways:

- **WO Structure**: Changes to the work order structure will update corresponding routes and associated PMs.
- **Classification and Task Names**: Update the classification and task names, which will adjust future PM tasks accordingly.
- **Parameter Values**: Modify parameter values and their weightage percentages, affecting the PM frequency calculations.

### 4. Automatic Updates
The configurator ensures that changes to configurations are automatically reflected in the PM records:

- **Route Records**: When an asset moves between operating locations and storerooms, route records are updated accordingly.
- **Frequency Parameters**: Updates to frequency parameters for locations trigger updates to associated PMs.

### 5. Business Service Process Flow
The business user can create and configure new PM configurations or update existing ones in the Configurator Application. The configurations define how PMs should exist in Maximo and how work orders and tasks will be created based on the following set of values:

| Configuration Type | Possible Values                                  | Remarks                                                                 |
|--------------------|--------------------------------------------------|-------------------------------------------------------------------------|
| PM Type            | Telecom PM, Cooling PM, Power PM, Baseload Genset PM | Required for creating a new configuration. Cannot be modified later.    |
| Location Type      | Mobile Access, Exchange/Building                 | Required for creating a new configuration. Cannot be modified later.    |
| WO Structure       | One WO per asset with Single Task, One WO per site with One Task per asset, One WO per site with standard single Task | Can be modified later; updates associated PMs and future tasks.         |
| Section            | Various Etisalat sections                        | Required for creating a new configuration. Cannot be modified later.    |
| Sub-section        | Various sub-sections of selected section         | Required for creating a new configuration. Cannot be modified later.    |
| Frequency Type     | Fixed, Dynamic                                   | Can be modified later.                                                  |
| Asset Technology   | Various asset technologies                       | Non-required for creating a new configuration. Cannot be modified later.|
| Classification     | Various Etisalat Asset classifications           | Required for creating a new configuration. Can be modified later.       |
| Task Name          | Various FOP task names                           | Required for each classification. Can be modified later.                |

### 6. Design Specifications
- Users can view and filter existing configurations.
- The system automatically creates or updates PM and route records based on defined rules.
- User prompts and validations ensure accuracy and completeness of configurations.



In the PM Configurator, the dynamic and fixed frequency types work as follows:

### Dynamic Frequency
- **Dynamic Frequency** allows for a more flexible approach where the frequency of PMs (Preventive Maintenance) is determined by multiple parameters and their associated weightages.
- Users can select from a list of predefined parameters and assign a weightage percentage to each. The total weightage must sum up to 100%.
- Based on these parameters and their values, an overall weightage for the location is calculated. The applicable weightage range is then identified, and the frequency defined for this range is set for the PM.
- This approach enables the PM frequency to adjust dynamically based on changes in the parameter values, providing a more tailored maintenance schedule.

### Fixed Frequency
- **Fixed Frequency** is a simpler approach where the PMs are scheduled at a constant interval.
- Users specify a fixed frequency value (e.g., every 30 days), and the PMs are generated at this interval regardless of any changes in the parameter values.
- This method is straightforward and easy to implement, but it lacks the flexibility to adapt to varying conditions that might affect the maintenance needs.

### Key Steps for Dynamic Frequency Configuration
1. **Select Parameters**: Choose from the available list of parameters relevant to the maintenance needs.
2. **Assign Weightages**: Allocate weightage percentages to each selected parameter. Ensure the total sums up to 100%.
3. **Define Frequency Ranges**: Set frequency ranges based on the calculated overall weightage from the parameters.
4. **Automatic Adjustments**: The system will automatically update the PM schedules based on changes in parameter values, recalculating the overall weightage and applying the corresponding frequency range.

### Key Steps for Fixed Frequency Configuration
1. **Specify Frequency Value**: Directly enter the desired interval for PM generation.
2. **Consistency**: PMs will be generated at this fixed interval without any changes unless the frequency value is manually updated.

These configurations ensure that maintenance schedules can either be consistent and straightforward (fixed) or adaptable and responsive to changing conditions (dynamic).

### Example Configuration Process
1. **Create Configuration**:
    - Select PM Type (e.g., Telecom PM, Cooling PM, Power PM, Baseload Genset PM).
    - Choose Location Type (e.g., Mobile Access, Exchange/Building).
    - Define WO Structure (e.g., One WO per asset with Single Task).
    - Select Section and Sub-section.
    - Choose Frequency Type (Dynamic or Fixed).
    - For Dynamic: Select and assign weightages to parameters, and define frequency ranges.
    - For Fixed: Enter the fixed frequency value.

2. **Validate and Apply Configuration**:
    - Validate the configuration settings.
    - The system will run a background job overnight to create or update PMs and route records based on the configuration rules.

3. **Update Configuration**:
    - Modify any parameters or values as needed.
    - The system will automatically adjust the PM schedules according to the new configuration settings.

This dynamic and fixed frequency approach in PM Configurator ensures that preventive maintenance can be both rigidly scheduled for consistency and dynamically adjusted for flexibility, depending on the organization's maintenance strategy.

### Dynamic Frequency Calculation in PM Configurator

The dynamic frequency type in PM Configurator involves assigning weightages to various parameters and using these weightages to determine the PM frequency range and cycle. Here’s a detailed breakdown of how the frequency range and cycle are calculated:

#### 1. **Selection and Weightage Assignment**:
   - **Frequency Parameters**: The user selects frequency parameters from a predefined list. There are 12 parameters to choose from, such as Site Category, Site Type, Structure Type, BTS Type, etc.
   - **Weightage Assignment**: The user assigns a weightage percentage to each selected parameter. The sum of these weightages must equal 100%.

#### 2. **Parameter Values and Weightages**:
   - For each parameter, the user defines possible values and assigns weightages to these values. The sum of the weightages for each parameter's values must also equal 100%.

#### 3. **Frequency Range Definition**:
   - The user defines the frequency ranges and associates each range with a specific frequency cycle. For instance, a weightage range of 0-20% might correspond to a PM cycle of 6 months, while a range of 21-40% might correspond to a 3-month cycle.

#### 4. **Dynamic Calculation**:
   - **Overall Weightage Calculation**: For each PM, the system calculates the overall weightage for the location. This is done by matching each parameter value defined in the configuration with the corresponding value of the PM's location and summing up the assigned weightages.
   - **Frequency Assignment**: The system then identifies the applicable weightage range and assigns the corresponding frequency cycle to the PM.

#### 5. **Work Order (WO) Generation**:
   - Based on the calculated frequencies, PM work orders are generated automatically. The interval of PM generation depends on the determined frequency cycle, which is derived from the weightage calculation.

### Example Workflow

1. **Configuration**: 
   - Select parameters: Site Type, BTS Type.
   - Assign weightages: Site Type (50%), BTS Type (50%).
   - Define parameter values and weightages: 
     - Site Type: Urban (30%), Rural (70%).
     - BTS Type: Type A (40%), Type B (60%).
   - Define frequency ranges: 
     - 0-20%: 12 months.
     - 21-40%: 6 months.
     - 41-60%: 3 months.
     - 61-80%: 1 month.
     - 81-100%: 2 weeks.

2. **Weightage Calculation**: 
   - For a location with Site Type 'Rural' and BTS Type 'Type B':
     - Site Type weightage = 70%.
     - BTS Type weightage = 60%.
     - Overall weightage = 70% + 60% = 130% (normalized if necessary).

3. **Frequency Assignment**:
   - Identify frequency range: 81-100%.
   - Assign frequency cycle: 2 weeks.

4. **PM Generation**:
   - PMs for this location will be generated every 2 weeks based on the assigned frequency cycle.

This approach ensures that PM frequencies are dynamically adjusted based on specific location and asset parameters, leading to a more tailored and efficient maintenance schedule.

## Diagrams

This tree diagram captures the overall structure and flow of the PM Configurator's business service process and design specifications, providing a clear and concise overview of the steps and components involved.
```
PM Configurator
├── Business Service Process Flow
│   ├── Create or Update PM Configuration
│   │   ├── PM Type
│   │   │   ├── Telecom PM
│   │   │   ├── Cooling PM
│   │   │   ├── Power PM
│   │   │   └── Baseload Genset PM
│   │   ├── Location Type
│   │   │   ├── Mobile Access
│   │   │   └── Exchange/Building
│   │   ├── WO Structure
│   │   │   ├── One WO per asset with Single Task
│   │   │   ├── One WO per site with One Task per asset
│   │   │   └── One WO per site with standard single Task
│   │   ├── Section
│   │   │   ├── Section A
│   │   │   ├── Section B
│   │   │   └── Section C
│   │   ├── Sub-section
│   │   │   ├── Sub-section 1
│   │   │   ├── Sub-section 2
│   │   │   └── Sub-section 3
│   │   ├── Frequency Type
│   │   │   ├── Fixed
│   │   │   └── Dynamic
│   │   ├── Asset Technology
│   │   │   ├── Technology A
│   │   │   ├── Technology B
│   │   │   └── Technology C
│   │   ├── Classification
│   │   │   ├── Classification X
│   │   │   ├── Classification Y
│   │   │   └── Classification Z
│   │   └── Task Name
│   │       ├── Task 1
│   │       ├── Task 2
│   │       └── Task 3
│   ├── Validate Configuration
│   │   ├── Background Job Execution
│   │   │   ├── Update Existing PMs and Routes
│   │   │   └── Create New PMs and Routes
│   └── Frequency Parameter Updates
│       ├── Dynamic Frequency Calculation
│       │   ├── Select Parameters
│       │   │   ├── Parameter 1
│       │   │   ├── Parameter 2
│       │   │   └── Parameter 3
│       │   ├── Assign Weightages
│       │   ├── Define Frequency Ranges
│       │   │   ├── Range 0-20%
│       │   │   │   └── Frequency: 12 months
│       │   │   ├── Range 21-40%
│       │   │   │   └── Frequency: 6 months
│       │   │   ├── Range 41-60%
│       │   │   │   └── Frequency: 3 months
│       │   │   ├── Range 61-80%
│       │   │   │   └── Frequency: 1 month
│       │   │   └── Range 81-100%
│       │   │       └── Frequency: 2 weeks
│       └── Fixed Frequency Specification
│           └── Set Fixed Interval
│               ├── Interval: 30 days
│               ├── Interval: 60 days
│               └── Interval: 90 days

├── Design Specifications
│   ├── Fixed Frequency
│   │   ├── Define Fixed Interval
│   │   │   ├── Enter Interval (e.g., 30 days)
│   │   │   └── PMs Generated at Fixed Intervals
│   ├── Dynamic Frequency
│   │   ├── Select Parameters
│   │   │   ├── Parameter 1 (e.g., Site Type)
│   │   │   ├── Parameter 2 (e.g., BTS Type)
│   │   │   └── Parameter 3 (e.g., Site Category)
│   │   ├── Assign Weightages
│   │   │   ├── Site Type: Urban (30%), Rural (70%)
│   │   │   ├── BTS Type: Type A (40%), Type B (60%)
│   │   │   └── Site Category: Category 1 (50%), Category 2 (50%)
│   │   ├── Define Frequency Ranges
│   │   │   ├── Range 0-20%: 12 months
│   │   │   ├── Range 21-40%: 6 months
│   │   │   ├── Range 41-60%: 3 months
│   │   │   ├── Range 61-80%: 1 month
│   │   │   └── Range 81-100%: 2 weeks
│   │   ├── Calculate Overall Weightage
│   │   │   ├── Sum of Parameter Weightages
│   │   │   └── Map to Frequency Range
│   │   └── Generate PMs Based on Calculated Frequency

```
Here’s a tree diagram that illustrates the scenarios where new PMs (Preventive Maintenance) and routes get created, and when existing PMs and routes get updated:

```plaintext
PM Configurator
├── Scenarios
│   ├── Create New PMs and Routes
│   │   ├── New Configuration
│   │   │   ├── PM Type
│   │   │   │   ├── Telecom PM
│   │   │   │   ├── Cooling PM
│   │   │   │   ├── Power PM
│   │   │   │   └── Baseload Genset PM
│   │   │   ├── Location Type
│   │   │   │   ├── Mobile Access
│   │   │   │   └── Exchange/Building
│   │   │   ├── WO Structure
│   │   │   │   ├── One WO per asset with Single Task
│   │   │   │   ├── One WO per site with One Task per asset
│   │   │   │   └── One WO per site with standard single Task
│   │   │   ├── Section
│   │   │   │   ├── Section A
│   │   │   │   ├── Section B
│   │   │   │   └── Section C
│   │   │   ├── Sub-section
│   │   │   │   ├── Sub-section 1
│   │   │   │   ├── Sub-section 2
│   │   │   │   └── Sub-section 3
│   │   │   ├── Frequency Type
│   │   │   │   ├── Fixed
│   │   │   │   └── Dynamic
│   │   │   ├── Asset Technology
│   │   │   │   ├── Technology A
│   │   │   │   ├── Technology B
│   │   │   │   └── Technology C
│   │   │   ├── Classification
│   │   │   │   ├── Classification X
│   │   │   │   ├── Classification Y
│   │   │   │   └── Classification Z
│   │   │   └── Task Name
│   │   │       ├── Task 1
│   │   │       ├── Task 2
│   │   │       └── Task 3
│   │   └── No Existing PM or Route Matches Configuration
│   │       ├── New Location Added
│   │       ├── New Asset Classification
│   │       └── New Technology Introduced
│   ├── Update Existing PMs and Routes
│   │   ├── Existing Configuration Updated
│   │   │   ├── Frequency Update
│   │   │   │   ├── Fixed Frequency
│   │   │   │   └── Dynamic Frequency
│   │   │   │       ├── Parameter Weightage Change
│   │   │   │       ├── Frequency Range Update
│   │   │   │       └── Overall Weightage Recalculation
│   │   │   ├── Task Name Update
│   │   │   ├── Asset Technology Update
│   │   │   └── Classification Update
│   │   └── Location or Asset Changes
│   │       ├── Location Type Change
│   │       ├── Asset Addition or Removal
│   │       └── Classification Change
│   └── Related Information
│       ├── Background Job Execution
│       │   ├── Runs Overnight
│       │   └── Performs Configuration Checks
│       ├── Validation Process
│       │   ├── Validates Configuration Rules
│       │   └── Ensures Data Integrity
│       ├── Frequency Types
│       │   ├── Fixed Frequency
│       │   │   └── Set Interval (e.g., 30 days)
│       │   └── Dynamic Frequency
│       │       ├── Parameter Selection
│       │       ├── Weightage Assignment
│       │       ├── Frequency Range Definition
│       │       └── Overall Weightage Calculation
│       └── Work Order (WO) Generation
│           ├── Based on Frequency Type
│           │   ├── Fixed: Constant Interval
│           │   └── Dynamic: Calculated Interval
│           └── PM Scheduling
│               ├── Regular Intervals
│               └── Adjustments Based on Parameter Changes
```

This tree diagram outlines the scenarios for creating new PMs and routes, updating existing PMs and routes, and provides related information about the background job execution, validation process, frequency types, and work order generation.

```
PM Configurator
├── Scenarios
│   ├── Create New PMs and Routes
│   │   ├── New Configuration
│   │   │   ├── PM Type
│   │   │   │   ├── Telecom PM
│   │   │   │   ├── Cooling PM
│   │   │   │   ├── Power PM
│   │   │   │   └── Baseload Genset PM
│   │   │   ├── Location Type
│   │   │   │   ├── Mobile Access
│   │   │   │   └── Exchange/Building
│   │   │   ├── WO Structure
│   │   │   │   ├── One WO per asset with Single Task
│   │   │   │   ├── One WO per site with One Task per asset
│   │   │   │   └── One WO per site with standard single Task
│   │   │   ├── Section
│   │   │   │   ├── Section A
│   │   │   │   ├── Section B
│   │   │   │   └── Section C
│   │   │   ├── Sub-section
│   │   │   │   ├── Sub-section 1
│   │   │   │   ├── Sub-section 2
│   │   │   │   └── Sub-section 3
│   │   │   ├── Frequency Type
│   │   │   │   ├── Fixed
│   │   │   │   └── Dynamic
│   │   │   ├── Asset Technology
│   │   │   │   ├── Technology A
│   │   │   │   ├── Technology B
│   │   │   │   └── Technology C
│   │   │   ├── Classification
│   │   │   │   ├── Classification X
│   │   │   │   ├── Classification Y
│   │   │   │   └── Classification Z
│   │   │   └── Task Name
│   │   │       ├── Task 1
│   │   │       ├── Task 2
│   │   │       └── Task 3
│   │   └── No Existing PM or Route Matches Configuration
│   │       ├── New Location Added
│   │       ├── New Asset Classification
│   │       └── New Technology Introduced
│   ├── Update Existing PMs and Routes
│   │   ├── Existing Configuration Updated
│   │   │   ├── Frequency Update
│   │   │   │   ├── Fixed Frequency
│   │   │   │   └── Dynamic Frequency
│   │   │   │       ├── Parameter Weightage Change
│   │   │   │       ├── Frequency Range Update
│   │   │   │       └── Overall Weightage Recalculation
│   │   │   ├── Task Name Update
│   │   │   ├── Asset Technology Update
│   │   │   └── Classification Update
│   │   └── Location or Asset Changes
│   │       ├── Location Type Change
│   │       ├── Asset Addition or Removal
│   │       └── Classification Change
│   └── Related Information
│       ├── Background Job Execution
│       │   ├── Runs Overnight
│       │   └── Performs Configuration Checks
│       ├── Validation Process
│       │   ├── Validates Configuration Rules
│       │   └── Ensures Data Integrity
│       ├── Frequency Types
│       │   ├── Fixed Frequency
│       │   │   └── Set Interval (e.g., 30 days)
│       │   └── Dynamic Frequency
│       │       ├── Parameter Selection
│       │       ├── Weightage Assignment
│       │       ├── Frequency Range Definition
│       │       └── Overall Weightage Calculation
│       └── Work Order (WO) Generation
│           ├── Based on Frequency Type
│           │   ├── Fixed: Constant Interval
│           │   └── Dynamic: Calculated Interval
│           └── PM Scheduling
│               ├── Regular Intervals
│               └── Adjustments Based on Parameter Changes

```

## Conclusion
The PM Configurator is a comprehensive tool designed to automate and manage preventive maintenance configurations effectively. By leveraging its features, users can ensure consistent and accurate PM scheduling, ultimately enhancing maintenance efficiency and reliability.