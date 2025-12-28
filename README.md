# cuiqgen - Quick Sample Data Generator

A fast, self-contained CLI tool for generating synthetic data in multiple formats. No external dependencies, no Python required.

## Features

- ✨ **Self-contained** - Single binary, no runtime dependencies
- 🚀 **High performance** - Generates millions of records efficiently
- 📦 **Multiple formats** - CSV, JSON, Parquet, SQLite, DuckDB
- 🔌 **Custom providers** - 70+ built-in data generators
- 🌍 **Local-first** - No external API calls
- 🛠️ **Cross-platform** - Windows, macOS, Linux
- 🔐 **Reproducible** - Seed support for deterministic output
- 📝 **AI-friendly** - Optional prompt-based generation (planned for 2026)
- 📝 **Relational models** - Generate relational models from configuration file (planned for 2026)
- 📝 **Basic Web UI** - Simple UI assistant (planned for 2026)

## Installation

Download precompiled binaries from [releases](https://github.com/cuiqanalytics/cuiqgen/releases).

## Quick Start

### Check commands

```bash
cuiqgen --help
```

### List providers

```bash
cuiqgen providers
```

**Tip**: Use a pager like `less` or `more` to view the list of providers.

### Generate sample data

```bash
cuiqgen run --number 1000 --providers "uuid;email;phone;country;amount(1,1000)" data.csv
```

## General usage

```
cuiqgen run [FLAGS] [FILENAME]
```

**Arguments:**
- `FILENAME` - Output file path (format detected by extension: .csv, .json, .parquet)

**Flags:**
- `-n, --number INT` - Number of records to generate (default: 100)
- `-p, --providers STRING` - Semicolon-separated provider names (default: uuid;first_name;last_name;email;phone;country)

**Examples:**

```bash
# Generate 1000 user records in CSV
cuiqgen run -n 1000 -p "uuid;first_name;last_name;email;phone" users.csv

# Generate 1000 user records in Excel
cuiqgen run -n 1000 -p "uuid;first_name;last_name;email;phone" users.xlsx

# Generate 5000 transaction records
cuiqgen run -n 5000 -p "uuid;amount(100,10000);currency;date('2020-01-01','2020-12-31')" transactions.csv

# Generate in JSON format with verbose output
cuiqgen run -n 500 -p "sku;product;price(1000,3000,'USD',100);currency" products.json

# Generate large dataset in Parquet
cuiqgen run -n 1000000 -p "uuid;country;amount(1,1000)" events.parquet
```

## Available Data Providers

```
Animals:
────────────────────────────────────────
animal_farm: generates a random farm animal
animal_petname: generates a random pet name
animal_type: generates a random animal type
cat_breed: generates a random cat breed

Banking:
────────────────────────────────────────
bank_account: generates a random bank account number
bank_name: generates a random bank name
iban: generates a random IBAN

Colors:
────────────────────────────────────────
color_safe: generates a random web-safe color

Common:
────────────────────────────────────────
amount: generates a random amount between low and high inclusive
bool: generates a random boolean
choice: generates a random selects a random element from an array [...elements...]
hex: generates a random hexadecimal digit
letter: generates a random letter
rgb_hex: generates a random RGB color in hexadecimal format
sentence: generates a random sentence

Currency:
────────────────────────────────────────
currency_code: generates a random currency code

Dates:
────────────────────────────────────────
date: generates a random date between two dates

Distributions:
────────────────────────────────────────
beta: generates a random value from Beta distribution (0-1 range)
exponential: generates a random value from exponential distribution with rate lambda
lognormal: generates a random value from lognormal distribution
normal: generates a random value from a normal distribution with given mean and standard deviation
pareto: generates a random value from Pareto distribution
poisson: generates a random approximate random value from Poisson distribution with parameter lambda
uniform: generates a random value from uniform distribution [a, b]
weibull: generates a random value from Weibull distribution

Identifiers_and_passwords:
────────────────────────────────────────
password: generates a random password
rut: generates a random chilean RUT
ssn: generates a random US Social Security Number
uuid: generates a random UUID

Language:
────────────────────────────────────────
language_code: generates a random language code

Location:
────────────────────────────────────────
country: generates a random country name
iso2: generates a random ISO 2 country code
lat: generates a random latitude
lon: generates a random longitude
street_prefix: generates a random street prefix
street_suffix: generates a random street suffix

Logging:
────────────────────────────────────────
apache_log_level: generates a random Apache log level
log_level: generates a random log level
syslog_level: generates a random syslog level

Numerical:
────────────────────────────────────────
float: generates a random float between a and b with specified precision `prec`
int: generates a random integer between a and b inclusive
serial_id: generates a random serial integer number in ascending order

Payments:
────────────────────────────────────────
payment_card_type: generates a random payment card type

Personal:
────────────────────────────────────────
email: generates a random email address
email_from_name: generates a random email address from first name and last name
first_name: generates a random first name
gender: generates a random gender
last_name: generates a random last name
name: generates a random full name
phone: generates a random phone number
prefix: generates a random name prefix
suffix: generates a random name suffix

Pharma:
────────────────────────────────────────
dose: generates a random dose
drug: generates a random drug
nrx: generates a random NRX

Products:
────────────────────────────────────────
category: generates a random category
currency: generates a random currency
price: generates a random price between `a` and `b`
product: generates a random product
sku: generates a random SKU

Tech:
────────────────────────────────────────
hacker_abbreviation: generates a random abbreviation
hacker_adjective: generates a random adjective
hacker_noun: generates a random noun
hacker_verb: generates a random verb

Vehicles:
────────────────────────────────────────
vehicle_fuel_type: generates a random vehicle fuel type
vehicle_maker: generates a random vehicle manufacturer
vehicle_transmission_type: generates a random vehicle transmission type
vehicle_type: generates a random vehicle type

Web:
────────────────────────────────────────
domain_suffix: generates a random domain suffix
http_method: generates a random HTTP method
http_status_code: generates a random HTTP status code from general set
http_status_simple: generates a random HTTP status code from simple set
internet_browser: generates a random web browser

Work:
────────────────────────────────────────
company: generates a random company name
job_descriptor: generates a random job descriptor
job_level: generates a random job level
job_title: generates a random job title
```

For detailed provider documentation, see [PROVIDERS.md](docs/PROVIDERS.md).

## Using Locales

Many providers support different locales for generating localized data. For example

```bash
# Generate spanish data
cuiqgen run -n 1000 --locale es -p "first_name('es');last_name('es');email;country" spanish_users.csv
```

**Supported locales**: Currently en, es. More locales will be added in the future.

## Preview Mode

Preview generated data before writing to a file:

```bash
# Preview 10 records without saving
cuiqgen run -p "uuid;first_name;last_name;email;phone" --preview
```

**Note**: Currently preview is fixed at 10 records.

## More Examples

### Generate E-commerce Product Data

You can customize the interval resolution for some functions, for example `price`:

```bash
cuiqgen run --preview -p "uuid;sku;product;category;price(1000,5000,'$',100);currency;amount(1,1000)"
```

### Generate Customer Transactions with Timestamps

```bash
cuiqgen run --preview -p "uuid;first_name;last_name;email;date('2023-01-01','2024-12-31');amount(5,10000);currency"
```

### Generate Server Logs

```bash
cuiqgen run --preview -p "date('2020-02-01','2020-03-01');http_status_code;http_method;float(0,5,2);internet_browser"
```

### Generate Healthcare Data

```bash
cuiqgen run --preview -p "uuid;first_name;last_name;ssn;phone;drug;dose;date('2023-01-01','2024-12-31')"
```

### Generate Financial Data with Distributions

```bash
cuiqgen run --preview -p "uuid;email;normal(50000,10000);exponential(0.001);currency;bank_name;iban"
```

### Generate Large Dataset in Parquet

```bash
cuiqgen run -n 20000000 \
  -p "uuid;first_name;last_name;email;phone;country;amount(100,10000)" \
  massive_dataset.parquet
```

### Generate Data with Custom Choices

```bash
cuiqgen run --preview -p "uuid;email;choice(['active','inactive','pending']);job_title;amount(50000,200000);currency"
```

### Generate Reproducible Data (Seeded)

```bash
# Generate with seed for reproducibility (it will produce the same data if you repeat the same command)
cuiqgen run --preview --seed 0.42 -p "uuid;first_name;last_name;email;phone"
```

## Performance

Generation speeds (on modern hardware):

| Records | Format  | Time   |
|---------|---------|--------|
| 10K     | CSV     | 0.05s  |
| 100K    | CSV     | 0.4s   |
| 1M      | CSV     | 4s     |
| 10M     | Parquet | 35s    |
| 100M    | Parquet | 5m     |

## Common Use Cases

### Generate Test Data for Development

```bash
cuiqgen run -n 1000 -p "uuid;first_name;last_name;email;phone;country" test_users.csv
```

### Create Sample Transactions

```bash
cuiqgen run -n 50000 -p "uuid;date('2024-01-01','2024-12-31');amount(100,5000);currency;bank_name" transactions.csv
```

### Generate Product Catalog

```bash
cuiqgen run -n 10000 -p "sku;product;price(1000,5000,'USD',100);currency" products.csv
```

### Testing Different Scenarios

```bash
# Generate test data multiple times
cuiqgen run -n 100 -p "uuid;email;amount(10,1000);date('2024-01-01','2024-12-31')" test_data.csv
```

## Troubleshooting

### "Provider not found" error

```bash
# List available providers
cuiqgen providers

# Check spelling - provider names are case-sensitive
cuiqgen run -p "uuid;first_name" data.csv  # ✓ correct
cuiqgen run -p "UUID;first_name" data.csv   # ✗ wrong (UUID should be lowercase)
```

### Out of memory with large datasets

For very large datasets (100M+ records), use Parquet format which is more memory-efficient:

```bash
cuiqgen run -n 1000000000 -p "uuid;amount(1,1000)" data.parquet
```

### Permission denied error

Ensure the output directory is writable:

```bash
chmod 755 /path/to/output
```

## Contributing

Suggestions are welcome!

## License

Free for personal or company non-commercial use. Check [LICENSE](LICENSE)

## Version

Current version: 0.1
