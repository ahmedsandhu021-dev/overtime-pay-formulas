# Overtime pay formulas

Plain formulas, worked examples and small code samples for calculating overtime pay. Figures are examples for learning, not legal or tax advice, and rules vary by state.

## The basic rule

Under the US Fair Labor Standards Act (FLSA), non-exempt employees must be paid at least 1.5 times their regular rate for hours worked over 40 in a workweek. Some states add daily overtime or double time, so check your state labor department.

Overtime pay = overtime hours x regular rate x 1.5

## Worked example

An employee earns $18 an hour and works 46 hours in one week.

| Line | Calculation | Amount |
|---|---|---|
| Regular pay | 40 x $18 | $720 |
| Overtime pay | 6 x $27 | $162 |
| Gross pay | | $882 |

## JavaScript

```js
function overtimePay(rate, hours, threshold = 40, multiplier = 1.5) {
  const regular = Math.min(hours, threshold);
  const overtime = Math.max(0, hours - threshold);
  return regular * rate + overtime * rate * multiplier;
}

overtimePay(18, 46); // 882
```

## Python

```python
def overtime_pay(rate, hours, threshold=40, multiplier=1.5):
    regular = min(hours, threshold)
    overtime = max(0, hours - threshold)
    return regular * rate + overtime * rate * multiplier

overtime_pay(18, 46)  # 882
```

## The regular rate is not always the hourly wage

Non-discretionary bonuses and shift differentials generally have to be included before the overtime premium is calculated.

Example: $20 an hour, 45 hours, and a $90 production bonus promised in advance.

- Straight-time pay: 45 x $20 = $900, plus $90 = $990
- Regular rate: $990 / 45 = $22.00
- Overtime premium: 5 hours x $22.00 x 0.5 = $55
- Total pay: $990 + $55 = $1,045

```js
function overtimeWithBonus(rate, hours, bonus, threshold = 40) {
  const straightTime = rate * hours + bonus;
  const regularRate = straightTime / hours;
  const overtimeHours = Math.max(0, hours - threshold);
  return straightTime + overtimeHours * regularRate * 0.5;
}

overtimeWithBonus(20, 45, 90); // 1045
```

## Tax note

For tax years 2025 through 2028, the premium part of qualifying overtime pay may be deductible on a federal return, up to $12,500 a year ($25,000 for joint filers), with phase-outs at higher incomes. Only the extra half of time and a half counts. For example, 300 overtime hours at $18 an hour is $8,100 of overtime pay, and only the $2,700 premium portion could qualify. Check IRS guidance or a tax professional for your own situation.

## Free calculators

To check results without writing code, see the free [OT Pay Calculator](https://otpaycalculator.com/) and the [no tax on overtime calculator](https://otpaycalculator.com/no-tax-on-overtime/).
