# Using Indices for Complex Comparison

For the NICAR 2016 conference in Denver, Census Reporter's [Joe Germuska](https://about.me/JoeGermuska) participated in a panel, [The way we look next: Mining past and future census data to predict diversity in race, income and aging](https://www.ire.org/events-and-training/event/2198/2419/).

Joe's section was on Using Indices for Complex Comparison ([slides](https://docs.google.com/presentation/d/1DPNyDdZp6XwVgpkc-IrLb1Qd70Sd-j6xbeBmTujA5Y4/edit?usp=sharing)).

Much of the talk was intended to demonstrate how humans can use Census Reporter to compute the USA Today Diversity index easily. The slides include a walkthrough of using Microsoft Excel to do the work. This repository shows how you can do it with Python.

Below is some of what is also in the slideshow, besides the Excel demo.

## What is the USAT Diversity Index

* Created by Phil Meyer (UNC) and Shawn McIntosh (USAT) in 1991
* [Reviewed in 2001](http://www.unc.edu/~pmeyer/carstat/tools.html#updating) after Census changed race question. Equation essentially unchanged.

### The equation

Diversity = 1-((_WhitePct_<sup>2</sup> + _BlackPct_<sup>2</sup> + _AmericanIndianPct_<sup>2</sup> + _AsianPct_<sup>2</sup> + _NativeHawaiianPct_<sup>2</sup>) * (_HispanicPct_<sup>2</sup> + _NonHispanicPct_<sup>2</sup> ))

## Getting the data

The relevant data for these is in two tables
* [B02001 - Race](http://censusreporter.org/tables/B02001/)
* [B03003 - Hispanic or Latino Origin](http://censusreporter.org/tables/B03003/)

Census Reporter makes it easy to get Census Data for a variety of geographies. The links above take you to an overview page for each table, where you can enter the geography or geographies which you're analyzing.

If you work on this stuff for a while, you'll become familiar with the key _geoids_ (geographic identifiers) for the places you study most. You can learn some more about geoids and other aspects of how the Census Bureau deals with geography on [Census Reporter's geography help page](http://censusreporter.org/topics/geography/).

Another thing, if you work on this stuff for a while, is that you might just start "hacking" the URLs instead of going through the Census Reporter GUI. For example, say you've gotten the page for **B02001** for all states in the US:

    http://censusreporter.org/data/table/?table=B02001&geo_ids=040|01000US&primary_geo_id=01000US

To go from that page to _B03003 - Hispanic or Latino Origin_, you just have to change the value for table:

    http://censusreporter.org/data/table/?table=B03003&geo_ids=040|01000US&primary_geo_id=01000US

You can download the data from those pages in many formats, including Excel. Note that the Excel files do not include verbal labels for columns, because some of the column names are extremely long, or are nested so that making the individual column names clear would be clumsy. The full information about column names is included in a `JSON` file which is part of the download, but for your reference, these are the relevant columns for computing the diversity index:

* B02001002 White alone
* B02001003 Black or African American alone
* B02001004 American Indian and Alaska Native alone
* B02001005 Asian alone
* B02001006 Native Hawaiian and Other Pacific Islander alone

* B03003002 Not Hispanic or Latino
* B03003003 Hispanic or Latino

Since you need to compute percentages, note that, as is standard, the first column in each table is the "total" column, or the denominator. The values should be the same, because the _universe_ for both tables is the same. If somehow you find that they aren't, you've somehow gathered data from two different ACS releases. (That's very unlikely if you get data from Census Reporter for the same places at the same time.)

* B02001001 Total population
* B03003001 Total population

## Processing the data with Excel

A strictly verbal explanation of the process with Excel is tedious. See the [slides](https://docs.google.com/presentation/d/1DPNyDdZp6XwVgpkc-IrLb1Qd70Sd-j6xbeBmTujA5Y4/edit?usp=sharing) for an illustrated walkthrough.
