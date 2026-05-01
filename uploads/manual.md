# Zahl — User Manual

Zahl is a plain-text, natural-language calculator for macOS. Type expressions line by line; results appear instantly in the right column. Every sheet is saved automatically.

---

## Basic Arithmetic

Standard operators and natural language both work.

| Input | Result |
|---|---|
| `5 + 3` | `8` |
| `100 - 42` | `58` |
| `6 * 7` | `42` |
| `144 / 12` | `12` |
| `2 ^ 10` | `1024` |
| `10 / 3` | `3.333` |

Word forms are also accepted:

```
8 times 9          → 72
100 divided by 4   → 25
```

Parentheses group as expected:

```
(10 + 5) * 2       → 30
```

---

## Variables

Assign a value to a name and reuse it on any subsequent line. Variable names are case-sensitive.

```
price = 120
tax = price * 0.2
total = price + tax    → 144
```

Built-in constants:

| Name | Value |
|---|---|
| `pi` or `π` | 3.14159… |
| `tau` or `τ` | 6.28318… |
| `e` | 2.71828… |

---

## Comments

Lines beginning with `//` or `#` are ignored.

```
// this is a comment
# also a comment
price = 99
```

Plain text lines with no operators are treated as labels and produce no result.

---

## Percentages

```
20%                    → 20%        (percentage value)
20% of 80              → 16
80 + 20%               → 96         (80 plus 20% of 80)
80 - 20%               → 64
20% off 150            → 120
what percent of 80 is 20 → 25%
```

---

## Multiplier Words

```
twice 50               → 100
double 50              → 100
triple 50              → 150
half 80                → 40
half of 80             → 40
```

---

## Aggregation: `sum`, `average`, `mean`

Type `sum`, `average`, or `mean` alone on a line to aggregate all numeric results above it since the last blank line or previous aggregate. Blank lines reset the running total.

```
10 * 5                 → 50
8 + 6                  → 14
sum                    → 64

100
200
300
average                → 200
```

`average` and `mean` are interchangeable. Only plain numeric results are included — currency and unit results are excluded.

---

## The `prev` Keyword

`prev` always holds the numeric result from the line immediately above. It resets after a blank line or an error.

```
length = 12
width = 5
length * width         → 60
prev * 2               → 120
```

---

## Math Functions

Single-argument functions:

| Function | Description |
|---|---|
| `sqrt(x)` | Square root |
| `abs(x)` | Absolute value |
| `round(x)` | Round to nearest integer |
| `floor(x)` | Round down |
| `ceil(x)` | Round up |
| `log(x)` | Base-10 logarithm |
| `ln(x)` | Natural logarithm |
| `sin(x)` | Sine (degrees input) |
| `cos(x)` | Cosine (degrees input) |
| `tan(x)` | Tangent (degrees input) |

Two-argument functions:

| Function | Description |
|---|---|
| `min(x, y)` | Smaller of two values |
| `max(x, y)` | Larger of two values |
| `mod(x, y)` | Remainder of x ÷ y |

```
sqrt(144)              → 12
abs(-42)               → 42
round(3.7)             → 4
log(1000)              → 3
sin(30)                → 0.5
min(8, 13)             → 8
mod(17, 5)             → 2
```

---

## Hexadecimal, Binary & Octal

**Literals** — use prefixed notation directly in expressions:

```
0xFF                   → 255
0b1010                 → 10
0o17                   → 15
0xFF + 1               → 256
```

**Base display** — convert any number to a different base:

```
255 in hex             → 0xFF
10 in binary           → 0b1010
255 in octal           → 0o377
0xFF in decimal        → 255
```

---

## Currency Conversion

Rates update automatically from public exchange data (ECB, refreshed hourly). Use ISO 4217 codes. Either `to` or `in` connects source and target.

```
100 usd to eur
50 gbp in jpy
200 cad to thb
```

When the latest refresh fails but cached rates are available, Zahl still returns a value and marks it as cached:

```
100 usd to eur          → 90 EUR (cached 2026-04-24)
```

Supported codes: USD, EUR, GBP, JPY, CAD, AUD, CHF, CNY, HKD, NZD, SEK, NOK, DKK, SGD, MXN, INR, BRL, ZAR, TRY, KRW, THB, IDR, MYR, PHP, PLN, CZK, HUF, RON, ILS, AED, SAR, QAR, KWD, EGP, VND, UAH, PKR, BDT, RUB.

---

## Unit Conversion

Use `to` or `in` to convert between units of the same category.

### Length
`mm`, `cm`, `m`, `km`, `in`, `ft`, `yd`, `mi` (and full word forms)

```
5 km to miles          → 3.107 mi
6 feet to cm           → 182.88 cm
100 inches in meters   → 2.54 m
```

### Mass
`mg`, `g`, `kg`, `oz`, `lb`, `tonne`, `ton`

```
70 kg to lbs           → 154.324 lb
500 grams to oz        → 17.637 oz
```

### Volume
`ml`, `cl`, `dl`, `l`, `cup`, `pt`, `qt`, `gal`

```
2 liters to gallons    → 0.528 gal
1 gallon in liters     → 3.785 L
```

### Temperature
`c` / `celsius`, `f` / `fahrenheit`, `k` / `kelvin`

```
100 c to f             → 212 °F
37 celsius to kelvin   → 310.15 K
-40 f to c             → -40 °C
```

### Digital Data
`b`, `kb`, `mb`, `gb`, `tb` (SI) and `kib`, `mib`, `gib`, `tib` (binary)

```
1.5 gb to mb           → 1500 MB
512 mib to gib         → 0.5 GiB
```

### Energy
`j`, `kj`, `cal`, `kcal`, `wh`, `kwh`

```
500 kcal to kj         → 2092 kJ
3.6 kwh to j           → 12960000 J
```

### Area
`sqmm`, `sqcm`, `sqm`, `sqkm`, `sqin`, `sqft`, `sqyd`, `sqmi`, `acre` / `acres`, `ha` / `hectare`

```
1 sqkm to sqm          → 1000000 m²
2.5 acres to ha        → 1.012 ha
500 sqft to sqm        → 46.452 m²
```

### Angle
`deg` / `degree` / `degrees`, `rad` / `radian` / `radians`, `grad` / `gradian` / `gradians`

```
180 deg to rad         → 3.14159 rad
1 rad to deg           → 57.296 °
400 grad to deg        → 360 °
```

---

## Time Zone Conversion

```
14:30 EST in Berlin
9:00 am PST to Tokyo
now in London
```

Common timezone identifiers: `UTC`, `GMT`, city names (`London`, `Tokyo`, `Berlin`, `Sydney`, `Dubai`, `Singapore`), and IANA zone abbreviations (`EST`, `PST`, `CET`, `JST`, `HKT`, …).

---

## Date Arithmetic

### Relative dates
```
today
yesterday
tomorrow
```

### Date literals
```
Jan 15
Mar 15 2026
December 1
```

### Adding / subtracting time
```
today + 30 days
Jan 1 + 6 months
today - 2 weeks
Mar 15 2026 - 10 days
```

### Difference between dates
```
Mar 15 to Apr 30 in days
Jan 1 2026 to Dec 31 2026 in months
```

### Next / last weekday
```
next Monday
last Friday
next Wednesday
```

### Business days
```
today + 5 business days
Mar 1 + 10 business days
```

---

## Duration Conversion

Convert time durations between units.

```
3 hours in minutes     → 180 min
90 minutes in hours    → 1.5 hr
2 weeks in days        → 14 days
```

Supported units: `s` / `sec` / `seconds`, `m` / `min` / `minutes`, `h` / `hr` / `hours`, `days`, `weeks`, `mo` / `months`, `yr` / `years`.

---

## Relative Amount Expressions

```
100 more than 40       → 140
30 less than 200       → 170
```

---

## Sheets

Each sheet is an independent scratchpad saved automatically.

| Action | How |
|---|---|
| New sheet | `⌘T` or click `+` in the bottom bar |
| Switch sheet | Click the tab |
| Rename sheet | Double-click the tab name |
| Delete sheet | Click `×` on the tab |
| View all sheets | Click `≡` (appears when tabs overflow) |

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `⌘T` | New sheet |
| `⌘⇧K` | Clear current sheet (with confirmation) |
| `⌘⇧R` | Copy all results to clipboard |
| `⌘⇧E` | Copy sheet content + results to clipboard |
| `⌘⇧Space` | Focus/open Zahl globally (if enabled in Settings) |

---

## Settings

Open via the gear icon (bottom-left) or **File → Settings…**

### General

| Setting | Description |
|---|---|
| **Precision** | Number of decimal places (`Auto` rounds intelligently) |
| **Always on top** | Keeps the window above all other windows |
| **Show in menu bar** | Adds a menu bar icon for quick access |
| **Global hotkey** | Enables a custom shortcut to focus/open Zahl from anywhere |

### Appearance

| Setting | Description |
|---|---|
| **Font** | Monospace font family and size |
| **Text** | Color of the text you type |
| **Background** | Canvas and window background color |
| **Results** | Color of result values in the right column |
| **Tab Bar** | Color of icons and labels in the bottom bar |
| **Sum** | Color used for `sum`, `average`, and `mean` result lines |

### License *(direct download version only)*

Enter your license key to activate Zahl. Once activated, the key and registration date are shown. Use **Deregister** to remove the license from this machine and free up one of your two allowed activations, so you can register on another computer.

---

## Number Formatting

Numbers are formatted with commas for thousands separators. With **Precision** set to Auto, trailing zeros are trimmed and very large or small numbers use compact notation. Set a fixed decimal count (0–8) to override.

---

## Tips

- Empty lines act as visual separators and reset the `sum` accumulator.
- Variables defined on one sheet are not shared with other sheets.
- Lines with only text (no operators or numbers) are treated as labels and show no result.
- `per` is a synonym for `/`: `120 km per hour` evaluates as `120`.
