---
title: "Common queries to the Core Reporting API"
#author: "Artem Klevtsov"
#date: "2015-08-11"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{Common Queries}
  %\VignetteEngine{knitr::rmarkdown}
  %\VignetteEncoding{UTF-8}
---



Here are several of the most common queries to the Core Reporting API. Note that the definitions only include dimensions, metrics, filters, and sort parameters. Anybody using these queries should fill in the date range.

Before you start you need to authorize and set dates range.

```r
authorize()
id <- "1234567"
start.date <- "30daysAgo"
end.date <- "yesterday"
```

## General Queries

### Users and Pageviews Over Time

This query returns the total users and pageviews for the specified time period. Note that this query doesn't require any dimensions. 

```r
get_ga(id, start.date, end.date,
       metrics = "ga:sessions,ga:pageviews")
```

### Mobile Traffic

This query returns some information about sessions which occurred from mobile devices. Note that "Mobile Traffic" is defined using the default segment ID -14. 

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:mobileDeviceInfo,ga:source",
       metrics = "ga:sessions,ga:pageviews,ga:sessionDuration",
       segment = gaid::-14)
```

### Revenue Generating Campaigns

This query returns campaign and site usage data for campaigns that led to more than one purchase through your site.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source,ga:medium",
       metrics = "ga:sessions,ga:pageviews,ga:sessionDuration,ga:bounces",
       segment = "dynamic::ga:transactions > 1")
```

## Users

### New vs Returning Sessions

This query returns the number of new sessions vs returning sessions.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:userType", metrics = "ga:sessions")
```

### Sessions by Country

 This query returns a breakdown of your sessions by country, sorted by number of sessions.
 
```r
get_ga(id, start.date, end.date,
       dimensions = "ga:country", metrics = "ga:sessions", sort = "-ga:sessions")
```
 
### Browser and Operating System

This query returns a breakdown of sessions by the Operating System, web browser, and browser version used.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:operatingSystem,ga:operatingSystemVersion,ga:browser,ga:browserVersion",
       metrics = "ga:sessions")
```

### Time on Site

This query returns the number of sessions and total time on site, which can be used to calculate average time on site.

```r
get_ga(id, start.date, end.date,
       metrics = "ga:sessions,ga:sessionDuration")
```

## Traffic Sources

### All Traffic Sources - Usage

This query returns the site usage data broken down by source and medium, sorted by sessions in descending order. 

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source,ga:medium",
       metrics = "ga:sessions,ga:pageviews,ga:sessionDuration,ga:exits",
       sort = "-ga:sessions")
```

### All Traffic Sources - Goals

This query returns data for the first and all goals defined, sorted by total goal completions in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source,ga:medium",
       metrics = "ga:sessions,ga:goal1Starts,ga:goal1Completions,ga:goal1Value,ga:goalStartsAll,ga:goalCompletionsAll,ga:goalValueAll",
       sort = "-ga:goalCompletionsAll")
```

### All Traffic Sources - E-Commerce

This query returns information on revenue generated through the site for the given time span, sorted by sessions in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source,ga:medium",
       metrics = "ga:sessions,ga:transactionRevenue,ga:transactions,ga:uniquePurchases",
       sort = "-ga:sessions")
```

### Referring Sites

This query returns a list of domains and how many sessions each referred to your site, sorted by pageviews in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source",
       metrics = "ga:pageviews,ga:sessionDuration,ga:exits",
       filters = "ga:medium == referral", sort = "-ga:pageviews")
```

### Search Engines

This query returns site usage data for all traffic by search engine, sorted by pageviews in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source",
       metrics = "ga:pageviews,ga:sessionDuration,ga:exits",
       filters = "ga:medium == cpa,ga:medium == cpc,ga:medium == cpm,ga:medium == cpp,ga:medium == cpv,ga:medium == organic,ga:medium == ppc",
       sort = "-ga:pageviews")
```

### Search Engines - Organic Search

This query returns site usage data for organic traffic by search engine, sorted by pageviews in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source",
       metrics = "ga:pageviews,ga:sessionDuration,ga:exits",
       filters = "ga:medium == organic",
       sort = "-ga:pageviews")
```

### Search Engines - Paid Search

This query returns site usage data for paid traffic by search engine, sorted by pageviews in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:source",
       metrics = "ga:pageviews,ga:sessionDuration,ga:exits",
       filters = "ga:medium == cpa,ga:medium == cpc,ga:medium == cpm,ga:medium == cpp,ga:medium == cpv,ga:medium == ppc",
       sort = "-ga:pageviews")
```

### Keywords

This query returns sessions broken down by search engine keywords used, sorted by sessions in descending order. 

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:keyword",
       metrics = "ga:sessions",
       filters = "ga:medium == organic",
       sort = "-ga:sessions")
```

## Content

### Top Content

This query returns your most popular content, sorted by most pageviews.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:pagePath",
       metrics = "ga:pageviews,ga:uniquePageviews,ga:timeOnPage,ga:bounces,ga:entrances,ga:exits",
       sort = "-ga:pageviews")
```

### Top Landing Pages

This query returns your most popular landing pages, sorted by entrances in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:landingPagePath",
       metrics = "ga:entrances,ga:bounces",
       sort = "-ga:entrances")
```

### Top Exit Pages

This query returns your most common exit pages, sorted by exits in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:exitPagePath",
       metrics = "ga:exits,ga:bounces",
       sort = "-ga:exits")
```

### Site Search - Search Terms

This query returns the number of sessions broken down by internal site search, sorted by number of unique searches for a keyword in descending order.

```r
get_ga(id, start.date, end.date,
       dimensions = "ga:searchKeyword",
       metrics = "ga:searchUniques",
       sort = "-ga:searchUniques")
```

## References

- [Core Reporting API - Common Queries](https://developers.google.com/analytics/devguides/reporting/core/v3/common-queries)
- [Dimensions & Metrics Explorer](https://developers.google.com/analytics/devguides/reporting/core/dimsmets)
