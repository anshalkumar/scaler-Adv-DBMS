# Scaler Advanced Database Management Systems (Adv-DBMS) - Lab 7

This workspace contains the implementation and exercises for **Lab 7** of the Advanced DBMS curriculum. It consists of four distinct sub-projects implementing core database engine components: a B-Tree Database Index, a Clock Sweep Cache Buffer Pool Manager, Dijkstra's Shunting-Yard parser for WHERE clauses, and an Abstract Syntax Tree (AST) SQL Query Parser.

---

## Workspace Structure

The project components are organized as follows:

```
.
├── Index/                     # B-Tree Database Index Implementation
│   ├── CMakeLists.txt         # Build configuration
│   └── main.cpp               # C++ code for B-Tree search, insert, and split
│
├── storage_buffer/            # Cache Eviction Buffer Pool Manager
│   ├── CMakeLists.txt         # Build configuration
│   └── main.cpp               # C++ implementation of Second-Chance (Clock Sweep)
│
├── StorageEngine/
│   └── lab7/
│       ├── dsy/               # Dijkstra's Shunting-Yard Converter & Evaluator
│       │   ├── README.md      # Algorithm notes and detailed walk-through
│       │   └── main.cpp       # Infix-to-postfix WHERE clause evaluator
│       │
│       └── queryParsing/      # SQL Lexer and AST query execution engine
│           ├── README.md      # Lexical analysis and AST representation notes
│           └── main.cpp       # SELECT query lexical analysis, AST parser, and engine
│
├── students.db                # SQLite 3 reference database
└── README.md                  # This build & execution guide
```

---

## Compilation & Run Guide

All components are written in standard C++17 and can be compiled using `g++` (GCC/Clang) or using `cmake`.

### 1. B-Tree Database Index

The B-Tree index component implements a generic templated key-value B-Tree supporting standard $O(\log n)$ search, sorted insertions, child-node splitting, and hierarchical tree visualization.

*   **Compile:**
    ```bash
    g++ -std=c++17 Index/main.cpp -o btree_demo
    ```
*   **Run:**
    ```bash
    ./btree_demo
    ```

### 2. Cache Eviction Buffer Pool Manager (Clock Sweep)

The buffer pool manager simulates a database page/record cache using the thread-safe **Second-Chance (Clock Sweep)** replacement algorithm. It features a thread-safe implementation with a background maintenance thread.

*   **Compile:**
    ```bash
    g++ -std=c++17 storage_buffer/main.cpp -lpthread -o buffer_demo
    ```
*   **Run:**
    ```bash
    ./buffer_demo
    ```

### 3. Dijkstra's Shunting-Yard WHERE Clause Evaluator

Converts a SQL `WHERE` clause written in infix notation (e.g. `id > 3 AND (age < 25 OR age >= 30)`) into postfix (Reverse Polish Notation) honoring operator precedence, then filters matching records.

*   **Compile:**
    ```bash
    g++ -std=c++17 StorageEngine/lab7/dsy/main.cpp -o dsy_demo
    ```
*   **Run:**
    ```bash
    ./dsy_demo
    ```

### 4. SQL Lexer & AST Query Executor

A recursive-descent query parser. It performs lexical tokenization of query strings, constructs an Abstract Syntax Tree (AST) representing the selection logic, and executes the AST queries against mock database rows.

*   **Compile:**
    ```bash
    g++ -std=c++17 StorageEngine/lab7/queryParsing/main.cpp -o parser_demo
    ```
*   **Run:**
    ```bash
    ./parser_demo
    ```
