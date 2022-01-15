# When to Defer Taxes?

## Introduction

Many people in the [Bogleheads](https://www.bogleheads.org) community, a
fantastic resource for investing advice, believe that it is almost always better
to defer taxes (_i.e._ contribute to
[Traditional](https://www.bogleheads.org/wiki/Traditional_IRA) accounts rather
than [Roth](https://www.bogleheads.org/wiki/Roth_IRA) accounts). I would like to
make the case against the notion that deferring taxes is best for people that
can "max out" their retirement accounts, like many individuals that read
Bogleheads can do.

### Who Said Traditional is Better?

From the Bogleheads's [general
guidelines](https://www.bogleheads.org/wiki/Traditional_versus_Roth#General_guidelines)
on Traditional vs. Roth:

> Using 100% traditional because, for most people, traditional will be better.

While this is probably correct, the typical Bogleheads reader is probably a
better saver.

### Who is the Typical Person?

* In 2018, the real median [household income in the
U.S.](https://en.wikipedia.org/wiki/Household_income_in_the_United_States) was
$63,179.
* In 2018, the [median
age](https://en.wikipedia.org/wiki/Demographics_of_the_United_States#Median_age_of_the_population)
is 38.2 years old.
* Between 2015 and 2020, the [expected life
expectancy](https://en.wikipedia.org/wiki/Demographics_of_the_United_States#Vital_statistics_2)
is 78.8 years.

## Argument

My core argument is based around [minimum required
distributions](https://www.bogleheads.org/wiki/Required_Minimum_Distribution)
(RMD). As the name suggests, these are IRS-mandated withdrawals from select
retirement accounts. If an investor puts too much money in tax-deferred
accounts, they might be forced to withdrawal large sums of money, which could be
heavily taxed. The alternative is to redirect those contributions to Roth
accounts, in which you pay taxes up-front and then (hopefully) never again.

## Figures

The following figures are generated with the `graph.py` utility. The values are
calculated with the `sim.calculate_assets` method. Variables are:

* Real Interest Rate (1% - 7%, should satisfy everyone)
* Years to Wait Before Deferring Taxes

The lines represent your total assets (estate) after taxes at death. The goal is
to maximize this value. The higher (vertically) the line the better. It should
be noted that lines (interest rates) are independent from one another. The total
assets will be vary widely between different interest rates. The lines are
normalized to fit between 0.0 and 1.0 so they can be easily compared.

The figure below shows the typical American. They make a little more than
$60k/year. Unlike the typical American though, they attempt to max out their
retirement accounts. This figure shows that if you expect the long-term real
interest rate to be 6% or higher, you might be better off making Roth
contributions for a few years.

![Figure 1](https://github.com/6a74/finance/blob/master/figures/figure_01.png?raw=true)

Though, if the same person in the figure above were to have $100k already saved
in their traditional retirement accounts, the outcome would be quite different.
The (relatively) small amount grows exponentially and requires higher RMDs.

![Figure 2](https://github.com/6a74/finance/blob/master/figures/figure_02.png?raw=true)

Next, we have a slightly younger person, 25, that is just starting their career.
They have nothing in their retirement, but they graduated without debt and got a
decent job out of college making approximately $60k/year. With long-term
interest rates of 5%, 6%, and 7% this person should prefer Roth contributions
for at least the first decade of their career.

![Figure 3](https://github.com/6a74/finance/blob/master/figures/figure_03.png?raw=true)

Say the same recent graduate got a job making $100k/year instead of $60k/year.
What would change? Well, because of their higher income, traditional IRA
contributions are not deductible. There is no point in contributing to a
non-deductible IRA. Instead, they would contribute to a Roth IRA. For this
reason, it appears that this person would get less out of Roth contributions
than the previous lad.

![Figure 4](https://github.com/6a74/finance/blob/master/figures/figure_04.png?raw=true)

Next, let's say the person above has a coworker that is the same age and has the
same income, _but_ but spend twice as much (from $30k to $60k). What would
change? Well, not much honestly. Their tax-advantaged savings should be on par,
just their taxable savings would be different.

![Figure 5](https://github.com/6a74/finance/blob/master/figures/figure_05.png?raw=true)

Next, assume one of these lads were real lucky and got an internship at a nice
company during college, and somehow they found a way to sock away $100k into
their traditional retirement accounts. This definitely pushes the scale towards
Roth contributions for the beginning of their career.

![Figure 6](https://github.com/6a74/finance/blob/master/figures/figure_06.png?raw=true)

Let's jump back to the typical American, but say this person really wants to
retire early, say at 50 years old instead of 60. Unless their investments can
provide a 7% real return, they will probably be better off purely contributing
to traditional retirement accounts.

![Figure 7](https://github.com/6a74/finance/blob/master/figures/figure_07.png?raw=true)

On the other hand, what if the typical American decides to work a little bit
longer, till the age of 70. Will this change things? By golly, it will. Unless
their investments do very poorly over a long time, this person will be better
off starting with Roth contributions.

![Figure 8](https://github.com/6a74/finance/blob/master/figures/figure_08.png?raw=true)

Next, let's say there's a hot-shot kid in Silicon Valley making $300/year and
they want to retire at 40. Because they will have so few years in the workforce,
traditional contributions will not make much of a difference in terms of RMDs.
And because of their very high income, tax deductions are very valuable. These
deductions do more good than RMDs do bad.

![Figure 9](https://github.com/6a74/finance/blob/master/figures/figure_09.png?raw=true)

Finally, let's say the same hot-shot kid decides he likes his job and wants to
work another twenty years. The outcome is still the same. This person should
always defer taxes. Their tax-rate is too high not too.

![Figure 10](https://github.com/6a74/finance/blob/master/figures/figure_10.png?raw=true)

### Key Takeaways

* It _does_ makes sense to defer taxes later in one's career, just not always
  immediately.
* In very low interest rate (1%) scenarios, it is almost always better to defer
  taxes immediately.
* If you plan to retire very early (40), it appears to be better to defer
  taxes immediately.
* If long-term interest rates are high (6%+), it appears to be better to
  make Roth contributes.

## Utilities

### `sim.py`

This module contains the core function: `calculate_assets`. Given all of the
initial variables (parameters), this function will simulate your portfolio and
return the value of your assets (estate) after taxes, with the assumption that
someone will inherit them. In the following figures, the following command was
used:

```
./sim.py --verbose
```

Here are all of the configurable options:

![Parameters](https://github.com/6a74/finance/blob/master/figures/sim_01.png?raw=true)

It will generate a very large table that looks like this:

![Life](https://github.com/6a74/finance/blob/master/figures/sim_02.png?raw=true)

At the end, there will be a summary table:

![Summary](https://github.com/6a74/finance/blob/master/figures/sim_03.png?raw=true)

### `graph.py`

This utility generates a graph of your possibilities. This graph is intended to
help you choose whether to make traditional or Roth contributions. It takes
almost the exact same arguments as the `sim.py` script, but there are a few
missing options like the `--start-with-roth=YEARS` option. To get started, run
the following command:

```
./graph.py
```

![Figure 1](https://github.com/6a74/finance/blob/master/figures/figure_01.png?raw=true)

## How Do I Test It Out?

You are encouraged to clone this repository and try this stuff out for yourself!
This way, you will be able to use your own personal numbers. I tried to include
options for anything that made sense. If there is something missing, please
create an issue or send me an email.

### Dependencies

* [python](https://docs.python.org/3/whatsnew/3.8.html) (3.8+)
* [matplotlib](https://matplotlib.org)
* [progressbar2](https://pypi.org/project/progressbar2/)
* [tablulate](https://pypi.org/project/tabulate/)

## Rules and Assumptions

Not trying to hide this stuff, but here are some gotchas. Most of this stuff
boils down to it being very difficult to predict the future. But some things
were intential design decisions.

### Income

* There are no gaps in employment.
* Pay raises are constant (unrealistic, I'm aware).
* Saving contributions will go up at the same rate as pay raises.
* Any excess income will go into a taxable account.

### Taxes

* Federal taxes only; no state tax, social security, medicare, etc.
* Standard duduction only.
* Only "single" and "married" filing statuses.
* No dependents; no charities.

### RMDs

* After retirement and before RMDs, you will do [Roth IRA
  conversions](https://www.bogleheads.org/wiki/Roth_IRA_conversion). This amount
  is automatically calculated to produce the lowest taxes. Note: this currently
  assumes your marital status does not change during this
  post-retirement/pre-RMDs period. I understand that will not work for everyone.
* During RMDs, you will withdrawal at least your standard deduction. This is
  amount is taxed at 0%.
* RMDs are transferred to a taxable account, where it grows at the same interest
  rate as retirement accounts.

### Other

* Interest is applied at the end of each year.
* The "market" has no volatility. Investments grow at a steady rate.
* Divorce is not possible. Once you are married, you are stuck that way.
* Taxable investments are never sold and therefore capital gains is take taken
  into account. I could see myself adding a "yearly cost of living" option and
  intelligently withdrawing from the best account. In this situation, capital
  gains could be calculated and included.
