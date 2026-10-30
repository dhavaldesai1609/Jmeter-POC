# JMeter POC - Apache JMeter Load Testing Proof of Concept

A working Proof of Concept demonstrating [Apache JMeter](https://jmeter.apache.org/) load testing with practical examples.

JMeter is a powerful open-source tool for performance testing of web applications, APIs, and more.

## Prerequisites

- Java 8+ installed
- [Apache JMeter](https://jmeter.apache.org/download_jmeter.cgi) 5.x

```bash
# Download and extract JMeter
# https://jmeter.apache.org/download_jmeter.cgi

# Or via package managers
# macOS
brew install jmeter

# Verify
jmeter --version
```

## Quick Start

### GUI Mode (for building / debugging tests)

```bash
jmeter
# then File → Open → test-plans/01-smoke-test.jmx
```

### Non-GUI (CLI) Mode – recommended for real runs

```bash
# Run smoke test and generate HTML report
jmeter -n -t test-plans/01-smoke-test.jmx -l results/smoke-results.jtl -e -o results/smoke-report

# Run load test
jmeter -n -t test-plans/02-load-test.jmx -l results/load-results.jtl -e -o results/load-report
```

> `-n` = non-GUI, `-t` = test plan, `-l` = results file, `-e -o` = generate HTML dashboard

## Examples Included

| Test Plan | Description |
|-----------|-------------|
| `test-plans/01-smoke-test.jmx` | Basic smoke test – 1 thread, simple GET |
| `test-plans/02-load-test.jmx` | Load test with Thread Group ramp-up |
| `test-plans/03-api-crud.jmx` | Full API CRUD flow (POST → GET → PUT → DELETE) |
| `test-plans/04-csv-parameterized.jmx` | Data-driven test using CSV Data Set Config |

## Project Structure

```
Jmeter-POC/
├── README.md
├── test-plans/
│   ├── 01-smoke-test.jmx
│   ├── 02-load-test.jmx
│   ├── 03-api-crud.jmx
│   └── 04-csv-parameterized.jmx
├── data/
│   └── users.csv               # Sample data for CSV Data Set
└── results/                    # Output directory (git-ignored)
```

## Key Concepts Demonstrated

- **Thread Groups** – virtual users and ramp-up
- **HTTP Request** samplers
- **Listeners** – View Results Tree, Summary Report, Aggregate Report
- **Assertions** – Response Code, Response Time, JSON Assertion
- **CSV Data Set Config** – data-driven testing
- **Timers** – Constant Timer / think time
- **JSON Extractor** – extract values for subsequent requests
- **HTML Dashboard Report** – generated with `-e -o`

## Useful CLI Flags

```bash
-n                  # Non-GUI mode
-t <file.jmx>       # Test plan file
-l <file.jtl>       # Results file
-e -o <folder>      # Generate HTML report after run
-Jthreads=50        # Override property (e.g. thread count)
-q <file.properties># Additional properties file
```

## Tips

1. **Never run heavy tests in GUI mode** – GUI is for development only.
2. Always use **CLI + HTML Dashboard** for real performance runs.
3. Keep the number of listeners low during actual tests (they consume memory).
4. Use **CSV Data Set** or **User Defined Variables** for parameterization.

## Useful Links

- [JMeter Official Docs](https://jmeter.apache.org/usermanual/index.html)
- [Building a Test Plan](https://jmeter.apache.org/usermanual/build-test-plan.html)
- [HTML Dashboard Report](https://jmeter.apache.org/usermanual/generating-dashboard.html)
