---
title: "Order Matching Engine"
summary: Ultra fast order matching engine written in Go
draft: false
tags: ["Go", "MySQL"]

---

# Order Matching Engine (Golang)

A high-performance order matching engine developed in Golang, tailored for trading systems. This engine ensures rapid pairing of buy and sell orders, with an efficiency rate of approximately 16,000 orders per second.

## **System Design and Features**:

### **Database Initialization**:
- Utilizes the `github.com/go-sql-driver/mysql` package for MySQL integration.
- Efficiently establishes a connection with the MySQL database.

### **Data Structures and Models**:
- **Order**: A comprehensive model representing trade orders with attributes such as order ID, price, quantity, timestamp, user ID, and instrument identifier (BitName).
- **TradeDetails**: A model capturing the intricate details of completed trades, including trade timestamps, executed price, buyer and seller details, and calculated brokerage.

### **Concurrency and Order Processing**:
- Incorporates Golang's goroutines and the `sync` package to achieve concurrent fetching of optimal buy and sell orders, maximizing throughput.
- Executes multiple iterations of the order matching loop until either buy or sell orders are exhausted or the price criteria aren't met.

### **Order Matching Logic**:
- Uses price and timestamp as primary criteria for matching.
- **Matching Scenarios**:
    1. **Equal Quantities**: Both the buy and sell orders are removed from their respective books.
    2. **Buy Quantity Exceeds**: The sell order is culled, while the buy order undergoes a proportional reduction.
    3. **Sell Quantity Exceeds**: The buy order is culled, while the sell order undergoes a proportional reduction.

### **Database Operations and Transaction Management**:
- The engine employs SQL transactions to ensure atomicity and data integrity.
- On successful order match, trade details are persisted into a `MASTER_LEDGER`.
- Efficient rollback mechanisms are in place to counteract any anomalies or discrepancies during transaction execution.

### **Error Handling**:
- Implements a robust error logging mechanism, providing insights into database connection issues, CRUD operations, and transactional discrepancies.

### **Performance Metrics**:
- At the culmination of its run, the engine delivers a performance report, showcasing the total elapsed time, rate of order processing (highlighting its capability of processing approximately 16,000 orders per second), and total iterations executed.
