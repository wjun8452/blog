#How to process text data by using command line?
* How to convert .xlsx to .csv?

  ```
  $ brew install gnumeric
  
  $ ssconvert Book1.xlsx newfile.csv
  Using exporter Gnumeric_stf:stf_csv
  
  $ cat newfile.csv 
  ```

  

* total lines

```
wc -l s.csv
  148812 s.csv
```
* how many vehicles?

```
cut -d, -f40 < s.csv | cut -d_ -f1 | sort | uniq | wc -l
    20103
```
* how many uniq versions?

```
cut -d, -f35 < s.csv | sort | uniq -c
   15 2.0.7409
48578 2.0.7409-P
 884 2.0.8084
10474 2.0.8084-P
  12 2.0.8254
  30 2.0.8277
   2 2.0.8277-P
   2 2.0.8289
  10 3.0.505.7646
 299 3.0.505.7655
76160 3.0.505.7655-P
  80 3.0.507.7693
2438 3.0.507.7693-P
   6 3.0.7578
7367 3.0.7578-P
  84 3.3.102.8555
 112 3.3.102.8632
   1 3.3.102.8632-P
   1 3.3.102.8634
  11 3.3.102.8645
  26 4.0.140.1.10977
   3 4.0.140.1.10977-P
  11 4.0.141.1.11340
   2 4.0.141.1.11340-P
  15 4.0.141.3.11631
   9 4.0.142.3.11901
  19 4.0.142.3.11901-P
  17 4.0.143.3.12119
   1 4.0.143.3.12131
   1 4.0.144.1.12229
 168 4.0.144.1.12279
 424 4.0.144.1.12303
  31 4.0.144.1.12303-P
  56 4.0.144.1.12313
  36 4.0.144.1.12314
   4 4.0.144.3.000
 523 4.0.144.3.12277
   1 4.0.144.3.12277-P
 210 4.0.144.3.12296
 172 4.0.144.3.12306
 173 4.0.144.3.12314
 289 4.0.144.3.12315
  45 4.0.145.1.000
  10 5.0.145.1.21214
   1 app_version
```


* how many info3.2 vehicles?

```
$ grep -E '2\.0\.8084-P|2\.0\.7409-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
     12526
     
grep -E '2\.0\.8084-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
     379

grep -E '2\.0\.7409-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
   12148

```

* how many info3.2 failed?

```
$ grep -E '2\.0\.8084-P' s.csv | awk -F, '{if($1=="PREPARE_DATA" && $24=="FAIL") {print $40}}' | cut -d_ -f1 | sort| uniq | wc -l
       9

```

* how many info3.4 vehicles?

```
$ grep -E '3\.0\.505\.7655-P|3\.0\.507\.7693-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
    4661
grep '3\.0\.505\.7655-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
    4506
grep '3\.0\.507\.7693-P' s.csv | cut -d, -f40 | cut -d_ -f1 | sort | uniq | wc -l
      157
```

* how many info3.4 failed?

```
$ grep -E '3\.0\.505\.7655-P|3\.0\.507\.7693-P' s.csv | awk -F, '{if($1=="PREPARE_DATA" && $24=="FAIL") {print $40}}' | cut -d_ -f1 | sort| uniq | wc -l
    2531

$ grep -E '3\.0\.505\.7655-P|3\.0\.507\.7693-P' s.csv | awk -F, '{if($1=="PREPARE_DATA" && $24=="PASS") {print $40}}' | cut -d_ -f1 | sort| uniq | wc -l
       1

```
* how many info3.2 vehicles upgraded to 17Q1 and 17Q3?

```
grep -E '2\.0\.8084-P|2\.0\.7409-P' s.csv | awk -F, '{if($1=="MAP_UPDATE_SUCCESSFULLY_BOOTED" && $44=="DEN1-CN38-371-362-S305") {print $40,$44}}' | cut -d ' '  -f1 | cut -d_ -f1 | sort | uniq | wc -l
81

grep -E '2\.0\.8084-P|2\.0\.7409-P' s.csv | awk -F, '{if($1=="MAP_UPDATE_SUCCESSFULLY_BOOTED" && $44=="DEN1-CN38-373-371-8A12") {print $40,$44}}' | cut -d ' '  -f1 | cut -d_ -f1 | sort | uniq | wc -l
191

```

* how many info3.4 vehicles upgraded to 17Q3?

```
grep -E '3\.0\.505\.7655-P|3\.0\.507\.7693-P' s.csv | awk -F, '{if($1=="MAP_UPDATE_SUCCESSFULLY_BOOTED" && $44=="DEN1-CN38-373-371-8A12") {print $40,$44}}' | cut -d ' '  -f1 | cut -d_ -f1 | sort | uniq | wc -l
 1
```



* how many transaction tags?

```
cut -d, -f44 < s.csv | sort | uniq -c
123246 
1246 DEN1-CN38-371-362-S305
22879 DEN1-CN38-373-371-8A12
 729 DEN1-CN38-374-373-8S15
 712 DEN1-CN38-381-374-8D22
   1 transaction_tag
```
* how many uniq events?

```
cut -d, -f1 < s.csv | sort | uniq
CHECK_ENVIRONMENT
DOWNLOAD_DATA
FATAL_ERROR
GET_SPACE_INFO
MAP_UPDATE_SUCCESSFULLY_BOOTED
PREPARE_DATA
ROLLBACK
UPDATE_OK_TO_BOOT
UPDATE_START
event_name

```


* how to convert windows new line ^M to unix style?
```
$ perl -pi -e 's/\r\n?/\n/g' SGM_PROD_0312.csv
$ wc -l SGM_PROD_0312.csv
  144511 SGM_PROD_0312.csv
```

* issue2

```
$ cut -d, -f40 < s.csv | wc -l
cut: stdin: Illegal byte sequence
     102
```
* solution:

```
iconv -t UTF8//IGNORE -f ASCII SGM_PROD_0313.csv  > 0313.csv
```

* split text file

```
# split -l 120000 log.txt newlog    //通过指定行数，将日志分割成两个文件；
```




* headers

1. event_name
2. date_id	
3. log_id	
4. reg_vid	
5. visitor_id
6. carrier	
7. app_id	
8. utc_timestamp
9. time_zone
10. ad_id
11. os_version
12. connection_type
13. device_make
14. device_model
15. gps_state
16. map_source
17. current_lat
18. current_lon
19. nav_timestamp
20. speed
21. heading
22. duration
23. region
24. action
25. language
26. slogtime
27. manufacturer_id
28. car_id
29. current_city
30. current_state
31. current_country
32. model_year
33. vehicle_manufacturer
34. car_model
35. app_version
36. device_id	
37. base_transaction_tag
38. db_content
39. error_id
40. guid
41. layer
42. space_string
43. summary_id
44. transaction_tag
