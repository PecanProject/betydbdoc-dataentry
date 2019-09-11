## BETYdb-YABA and Python Client Library

BETYdb-YABA and its python client library provides an automated bulk upload to many BETYdb tables. API endpoints have been implemented to upload data to respective tables. For more information, see the BETYdb-YABA [README](https://github.com/PecanProject/BETYdb-YABA/blob/master/README.md) and [swagger documentation](https://app.swaggerhub.com/apis-docs/y51/bet-ydb_yaba/1.0.5).

Here are some examples of how to hit Experiments and Sites endpoints:

* Experiments:

```sh
curl -F "fileName=@input_files/experiments.csv"   \
     http://localhost:5001/yaba/v1/experiments?username=guestuser
```

* Sites:

```sh
curl -F "fileName=@input_files/sites.csv"   \
     -F "shp_file=@input_files/S8_two_row_polys.shp"  \
     -F "dbf_file=@input_files/S8_two_row_polys.dbf"  \
     -F "prj_file=@input_files/S8_two_row_polys.prj"  \
     -F "shx_file=@input_files/S8_two_row_polys.shx"  \
     http://localhost:5001/yaba/v1/sites
```

For examples of how to hit other endpoints, see the README.



