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

## Available Data Providers (76 total)

```
ANIMALS
────────────────────────────────────────
animal_farm(): farm animal
animal_petname(): pet name
animal_type(): animal type
cat_breed(): cat breed

BANKING
────────────────────────────────────────
bank_account(): bank account number
bank_name(): bank name
iban(): IBAN

COLORS
────────────────────────────────────────
color_safe(): web-safe color

COMMON
────────────────────────────────────────
amount(low,high,res): amount between `low` (integer) and `high` (integer), both inclusive, with specified resolution `res` (integer, default 1). For example: amount(1000,2000,100)
bool(): boolean (true or false)
choice(arr): random element from an array, for example: choice(['a','b','c'])
hex(): hexadecimal digit
letter(): letter
rgb_hex(): RGB color in hexadecimal format
sentence(words): sentence with `words` (default 10) random words

CURRENCY
────────────────────────────────────────
currency_code(): currency code

DATES
────────────────────────────────────────
date(min_date,max_date): date between two dates

DISTRIBUTIONS
────────────────────────────────────────
beta(α,β): value from Beta distribution (0-1 range) with parameters `α` and `β`
exponential(λ): value from exponential distribution with rate `λ`
lognormal(μ,σ): value from lognormal distribution with given mean `μ` and standard deviation `σ`
normal(μ,σ): value from a normal distribution with given mean `μ` and standard deviation `σ`
pareto(xmin,α): value from Pareto distribution with minimum value `xmin` and shape `α`
poisson(λ): approximate random value from Poisson distribution with parameter `λ`
uniform(a,b): value from uniform distribution between `a` and `b`
weibull(shape,scale): value from Weibull distribution with shape `shape` and scale `scale`

IDENTIFIERS_AND_PASSWORDS
────────────────────────────────────────
password(n): password with `n` characters (default 16)
rut(): chilean RUT
ssn(): US Social Security Number
uuid(): UUID

LANGUAGE
────────────────────────────────────────
language_code(): language code

LOCATION
────────────────────────────────────────
country(locale): country name with locale `locale` (default: en)
iso2(): ISO 2 country code
lat(): latitude
lon(): longitude
street_prefix(): street prefix
street_suffix(): street suffix

LOGGING
────────────────────────────────────────
apache_log_level(): Apache log level
log_level(): log level
syslog_level(): syslog level

NUMERICAL
────────────────────────────────────────
float(a,b,prec): float between `a` and `b` with specified rounding precision `prec` (default=2)
int(a,b): integer between a and b inclusive
serial_id(): serial integer number in ascending order

PAYMENTS
────────────────────────────────────────
payment_card_type(): payment card type

PERSONAL
────────────────────────────────────────
email(domain): email address with domain `domain` (default: @example.com)
email_from_name(first_name,last_name,domain): email address from first name and last name with domain `domain` (default: @example.com)
first_name(locale): first name with locale `locale` (default: en)
gender(extended): gender with optional `extended` flag (default: false)
last_name(locale): last name with locale `locale` (default: en)
name(): full name
phone(): phone number
prefix(): name prefix
suffix(): name suffix

PHARMA
────────────────────────────────────────
dose(): dose
drug(): drug
nrx(): NRX

PRODUCTS
────────────────────────────────────────
category(): category
currency(): currency
price(a,b,prefix,res): price between `a` and `b` with `prefix` (default $) and `res` (default 1)
product(): product
sku(): SKU

TECH
────────────────────────────────────────
hacker_abbreviation(): abbreviation
hacker_adjective(): adjective
hacker_noun(): noun
hacker_verb(): verb

VEHICLES
────────────────────────────────────────
vehicle_fuel_type(): vehicle fuel type
vehicle_maker(): vehicle manufacturer
vehicle_transmission_type(): vehicle transmission type
vehicle_type(): vehicle type

WEB
────────────────────────────────────────
domain_suffix(): domain suffix
http_method(): HTTP method
http_status_code(): HTTP status code from general set
http_status_simple(): HTTP status code from simple set
internet_browser(): web browser

WORK
────────────────────────────────────────
job_descriptor(): job descriptor
job_level(): job level
job_title(locale): job title with locale `locale` (default: en)
```

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
