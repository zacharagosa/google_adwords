### Block Info

_This Block is modeled on the schema brough in by Google's BigQuery Transfer Service. It will cover many of the core entities involved with the AdWords offering. Depending on how you use the DFP service, you may have additional entities brought in through thge BQ Transfer Service, especially any custom built reports. This Block should serve as a great jump start. Happy modeling!_

_The schema documentation for AdWords can be found in [Google's docs](https://developers.google.com/adwords/api/docs/guides/reporting#xml_schema_definition). Please note that your naming might vary slightly._

### Implementation Instructions

* **Sql_table_name** - in each of the views, the `sql_table_name` parameter must be changed to match your table names, particularly the tables with a wildcard operator when using `_table_suffix`. This must be changed in each view.
* **Dashboards** - rename the model in each LookML Dashboard element from "google_adwords" to the model name you've selected.


### Notes

* **Entity Tables vs Stat Tables** -tables with the "stats" suffix contain snapshot data by day, compiled into a large table. The values in these tables can be aggregated over time. These serve as our left-most tables, or "base tables", which we join our other tables onto with `many_to_one_joins`. The non-base (entity) tables are also running tables, but contain rolled-up data that cannot be aggregated over time. We restrict these tables using the `_latest_date = data_date` parameter in the `sql_table_name` clause. Avoid the use of `one_to_many` joins from base table to stat table, since stat tables have no primary key, and therefore cannot be aggregated over correctly during fanouts.
* **Included Entities** As mentioned above, this Block covers many to of core entities for AdWords (namely, `Ads`, `Keywords`, and `Campaigns`). Additional fields should be brought in as needed. The modeling logic applied to the core entities should also be applied any additional tables brought in via Transfer Services.
