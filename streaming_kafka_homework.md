- Generate this dataset with data-generator https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip to Kafka topic `iot-temp-raw` .

- Build a Spark Structured Streaming Application that consumes `iot-temp-raw` topic, enriches messages then produces `iot-temp-enriched` topic.
  - Enrich the message: Using event time (noted_date column)  by adding year, month, and day of week.
  - Produce results to `iot-temp-enriched` topic.


- Sample of dataset
```commandline
id,room_id/id,noted_date,temp,out/in
__export__.temp_log_196134_bd201015,Room Admin,08-12-2018 09:30,29,In
__export__.temp_log_196131_7bca51bc,Room Admin,08-12-2018 09:30,29,In
__export__.temp_log_196127_522915e3,Room Admin,08-12-2018 09:29,41,Out
__export__.temp_log_196128_be0919cf,Room Admin,08-12-2018 09:29,41,Out
```