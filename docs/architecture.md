graph TD
    subgraph "Data Sources"
        A[SAP ERP - Material/Orders]
        B[Operator Logs - Field Swaps]
    end

    subgraph "Processing Layer (Power Query)"
        C{Data Cleaning}
        D[Standardize Timestamps]
        E[Merge SAP & Field Data]
    end

    subgraph "Analytics Engine (DAX)"
        F[Cycle Count Aggregation]
        G[RUL Forecasting Model]
    end

    subgraph "Visual Output"
        H[Operator 'Health Bar' View]
        I[Executive Cost Dashboard]
    end

    A & B --> C
    C --> D --> E
    E --> F --> G
    G --> H & I
