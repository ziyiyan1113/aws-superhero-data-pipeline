# Superhero Data Pipeline with AWS Aurora, Lambda, and S3

This project demonstrates a simple serverless data pipeline using AWS services — Aurora MySQL, Lambda, and S3 — to simulate a real-world database + compute setup.

## 🔧 Tech Stack

- **AWS Aurora (MySQL-Compatible)** – Relational database for storing hero data
- **AWS Lambda** – Serverless compute to query and return data
- **Amazon S3** – Stores uploaded CSV data to be loaded into Aurora
- **EC2** – Used for setup and testing via terminal
- **IAM** – Roles & policies to allow S3 → Aurora integration
- **Redis (optional)** – For caching and performance improvement
- **Python** – Used in Lambda with `pymysql` and `redis` packages

---

## 📁 Project Structure

.
├── lambda_function.py # Main Lambda function handler
├── lambda_layer.zip # Layer containing pymysql and redis
├── week5_data.csv # Main CSV data uploaded to S3
├── test.csv # Sample CSV for testing S3 → Aurora connection
├── README.md # This documentation

---

## ✅ What’s Implemented

### ✔️ Data Setup

- [x] Created Aurora MySQL DB Cluster (`ziyi-cluster`)
- [x] Created `heroes` database and `hero_data` table
- [x] Uploaded sample `test.csv` and real `week5_data.csv` to S3
- [x] Verified S3 path and bucket (`ziyi-assignment-bucket`)
- [x] Assigned appropriate IAM role to Aurora (via parameter group)
- [x] Loaded CSV data into Aurora from S3 using:
  ```sql
  LOAD DATA FROM S3 's3://ziyi-assignment-bucket/week5_data.csv'
  INTO TABLE hero_data
  FIELDS TERMINATED BY ','
  LINES TERMINATED BY '\n'
  IGNORE 1 ROWS;
  
✔️ Lambda Setup

 - [x] Created Lambda function with Aurora connection
 - [x] Built lambda_layer.zip with pymysql and redis
 - [x] Attached layer to Lambda
 - [x] Tested Lambda with sample event and confirmed successful response

🧪 Sample Output

{
  "statusCode": 200,
  "body": {
    "results": [
      { "id": 1, "name": "irondoctor", "hero": "no", "power": "eat", "xp": 1000000, "color": "yellow" },
      { "id": 2, "name": "windhero", "hero": "no", "power": "grow", "xp": 999999, "color": "yellow" },
      { "id": 3, "name": "dogwoman", "hero": "maybe", "power": "steal", "xp": 999998, "color": "pink" }
    ],
    "execution_time": "0.0129s"
  }
}

🚀 Future Improvements

 - [x] Add Redis caching to improve performance for frequent queries
 - [x]  Connect via API Gateway for public HTTP endpoint
 - [x]  Add DynamoDB for NoSQL comparison
 - [x] Visualize data using Streamlit or other front-end framework


📌 Learning Outcomes

 - [x] Set up Aurora DB with S3 integration
 - [x] Handle IAM roles and permissions for secure resource access
 - [x] Work with Lambda layers and external Python packages
 - [x] Execute SQL queries via Lambda using pymysql
 - [x] Build end-to-end AWS-based mini data pipeline


📚 Resources

AWS Aurora Docs: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/

Lambda Layers: https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html

PyMySQL: https://pymysql.readthedocs.io/en/latest/


👤 Author

Ziyi Yan

