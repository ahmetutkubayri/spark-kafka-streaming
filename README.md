# Kafka & Spark Streaming Data Processing

This project contains two main data processing tasks using Apache Spark and Kafka:

1. **Streaming IoT Temperature Data with Kafka & Spark**
   - Reads real-time temperature data from Kafka.
   - Transforms the data by adding `Year`, `Month`, and `Day of the Week`.
   - Stores the enriched data in another Kafka topic.

2. **Order Status Analysis**
   - Finds the latest order status from an e-commerce dataset.
   - Outputs the results as a CSV file.
   - Includes visualizations of the processed data.

## 📁 Repository Structure

- `streaming_kafka_homework.md` → Explanation of the Kafka & Spark streaming task.
- `finding_the_latest_order_status.md` → Steps to analyze order statuses.
- `order_status_result.csv` → Processed order status data.
- `result_df.png` → Visualization of the result dataset.
- `source_data_view.png` → Screenshot of the source data before processing.

## 🔧 Prerequisites

To run this project, you need:

- **Docker** (for Kafka, Spark, and PostgreSQL)
- **Python 3** with `pyspark`, `pandas`, and `kafka-python` installed
- **Dataset from:**  
  ```
  https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip
  ```

## 🚀 Running the Kafka & Spark Streaming Task

1. Start the Kafka and Spark environment:
   ```bash
   docker-compose up -d
   ```

2. Download and copy the dataset:
   ```bash
   wget https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip
   unzip IOT-temp.csv.zip
   docker cp IOT-temp.csv kafka:/tmp/iot-temp-input/
   ```

3. Run the data generator:
   ```bash
   docker exec -it kafka bash
   cd /tmp/data-generator
   python3 dataframe_to_kafka.py -t iot-temp-raw -i /tmp/iot-temp-input/IOT-temp.csv -e csv -ks ','
   ```

4. Submit the Spark Streaming job:
   ```bash
   docker exec -it spark bash
   spark-submit /tmp/enrich_streaming.py
   ```

5. Verify the enriched data in Kafka:
   ```bash
   kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic iot-temp-enriched --from-beginning --max-messages 10
   ```

## 📊 Running the Order Status Analysis

1. Load the dataset into Spark.
2. Process the latest order statuses.
3. Write results to CSV format.
4. View the output in `order_status_result.csv`.

This project provides a hands-on experience in real-time data streaming and batch processing using Kafka and Spark.

