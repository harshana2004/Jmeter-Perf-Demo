# JMeter Performance Testing Demo

A practical Apache JMeter project demonstrating API performance testing, test data parameterisation, correlation, assertions, and multiple performance testing scenarios.

## Project Overview

This project uses Apache JMeter to performance test REST APIs and evaluate API behaviour under different levels of load.

The test includes:

* API performance testing
* CSV test data parameterisation
* Dynamic value extraction and correlation
* HTTP response assertions
* Transaction-level measurement
* Smoke testing
* Load testing
* Stress testing
* Spike testing
* Command-line execution
* JTL result collection
* HTML performance reporting

## Test API

The project uses the JSONPlaceholder REST API:

`https://jsonplaceholder.typicode.com`

### API Requests

| Request     | Method | Endpoint | Expected Response |
| ----------- | ------ | -------- | ----------------- |
| Get Users   | GET    | `/users` | 200               |
| Create Post | POST   | `/posts` | 201               |

## Test Data

CSV data is used to parameterise the POST request.

Example:

```csv
title,body,userId
Performance Test 1,Test data for user 1,1
Performance Test 2,Test data for user 2,2
Performance Test 3,Test data for user 3,3
Performance Test 4,Test data for user 4,4
Performance Test 5,Test data for user 5,5
```

JMeter reads the CSV values and passes them into the API request.

## Correlation

The GET Users response is used to demonstrate dynamic correlation.

A JSON JMESPath Extractor extracts a user ID from the API response:

```text
[0].id
```

The extracted value is stored in:

```text
${extractedUserId}
```

The extracted value can then be used by the subsequent POST request.

## Assertions

The test validates HTTP response codes to identify functional failures during performance testing.

### Get Users

Expected response:

```text
200
```

### Create Post

Expected response:

```text
201
```

## Performance Scenarios

Four performance scenarios were executed.

| Test   | Users | Ramp-up | Loops |
| ------ | ----: | ------: | ----: |
| Smoke  |     1 |   1 sec |     1 |
| Load   |    10 |  30 sec |     5 |
| Stress |    50 |  60 sec |     5 |
| Spike  |   100 |   1 sec |     2 |

### Smoke Test

Purpose: Verify that the test works correctly with minimal load.

```bash
jmeter -n -t api-load-test.jmx -Jusers=1 -Jrampup=1 -Jloops=1 -l results/smoke.jtl
```

### Load Test

Purpose: Evaluate API behaviour under expected concurrent load.

```bash
jmeter -n -t api-load-test.jmx -Jusers=10 -Jrampup=30 -Jloops=5 -l results/load.jtl
```

### Stress Test

Purpose: Evaluate API behaviour under increased load.

```bash
jmeter -n -t api-load-test.jmx -Jusers=50 -Jrampup=60 -Jloops=5 -l results/stress.jtl
```

### Spike Test

Purpose: Evaluate API behaviour when traffic increases rapidly.

```bash
jmeter -n -t api-load-test.jmx -Jusers=100 -Jrampup=1 -Jloops=2 -l results/spike.jtl
```

## HTML Report

The individual JTL results are combined and used to generate a JMeter HTML dashboard.

The generated report is located at:

```text
reports/performance-report/index.html
```

The combined results identify the performance scenarios as:

```text
Smoke | GET Users
Smoke | Create Post

Load | GET Users
Load | Create Post

Stress | GET Users
Stress | Create Post

Spike | GET Users
Spike | Create Post
```

## Project Structure

```text
jmeter-performance-demo/
│
├── api-load-test.jmx
│
├── data/
│   └── users.csv
│
├── results/
│   ├── smoke.jtl
│   ├── load.jtl
│   ├── stress.jtl
│   ├── spike.jtl
│   └── combined-results.jtl
│
├── reports/
│   └── performance-report/
│       └── index.html
│
├── .gitignore
└── README.md
```

Generated JTL files and HTML reports are excluded from Git using `.gitignore`.

## Technologies

* Apache JMeter 5.6.3
* Java
* REST API
* JSON
* CSV
* JMESPath
* Git
* GitHub

## Author

**Harshana Premarathna**

Senior QA / Test Automation Engineer with 17+ years of experience in software quality assurance, test automation, API testing, and quality engineering.

This project was created as a practical demonstration of JMeter performance testing and API quality engineering.

