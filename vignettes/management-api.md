---
title: "Obtain the access to the Management API"
#author: "Artem Klevtsov"
#date: "2015-08-11"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{Management API}
  %\VignetteEngine{knitr::rmarkdown}
  %\VignetteEncoding{UTF-8}
---



To access summary information of the Management API Google Analytics `RGA` package provides the following functions:

- `list_accounts()` - Lists all accounts which the user has access to;
- `list_webproperties()` - Lists web properties which the user has access to;
- `list_profiles()` - Lists views (profiles) which the user has access to;
- `list_custom_dimensions()` - Lists custom dimensions to which the user has access to;
- `list_custom_metrics()` - Lists custom metrics to which the user has access to;
- `list_custom_sources()` - List custom data sources which the user has access to;
- `list_experiments()` - Lists experiments to which the user has access to;
- `list_filters()` - Lists all filters for an account which the user has access to;
- `list_goals()` - Lists goals which the user has access to;
- `list_segments()` - Lists segments which the user has access to;
- `list_unsampled_reports()` - Lists unsampled reports which the user has access to;

Each of these functions return a table of data (`data.frame`) with the relevant content.

The functions such as `list_webproperties()`, `list_profiles()` and `list_goals()` can be specified with the additional arguments such as `account.id`, `webproperty.id` or `profile.id`  which are required to obtain the information for specific account, resource or profile (view the help pages for the corresponding functions). This is an example of obtaining the information on all views (profiles):

```r
list_profiles()
```

To get all profiles for a specific account try this:

```r
list_profiles(account.id = "XXXXXXXX")
```

To get a more detail information about interesing entry use following functions:

- `get_custom_dimension()` - Gets a custom dimension to which the user has access to;
- `get_custom_metric()` - Gets a custom metric to which the user has access to;
- `get_experiment()` - Gets a experiment to which the user has access to;
- `get_filter()` - Gets a filter to which the user has access to;
- `get_goal()` - Gets a goal to which the user has access to;
- `get_profile()` - Gets a view (profile) to which the user has access to;
- `get_webproperty()` - Gets a web property to which the user has access to;
- `get_unsampled_report()` - Gets a single unsampled report to which the user has access to;

Each of these functions return a set of data (`list`) with the relevant content.

To get information about specific filter in first you need obtain the filter ID with `list_filters()` function. Then use obtained filter ID to get more details about this filter:

```r
list_accounts()
list_filters(account.id = "XXXXXXXX")
get_filter(account.id = "XXXXXXXX", filter.id = "YYYYYYYY")
```

## References

- [What Is The Management API - Overview](https://developers.google.com/analytics/devguides/config/mgmt/v3/)
