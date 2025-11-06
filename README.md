<h1 align="center"> LogChain </h1>

LogChain is a secure and centralized log collection system that ensures the integrity of logs from various devices. 
Using AWS, it processes, stores, and queries critical logs while utilizing blockchain technology to guarantee the 
immutability and authenticity of log data. This project is a concept and still needs work!

<h2 align="center"> Project Overview </h2>

LogChain was developed with the objective of enhancing log security through blockchain technology. By implementing
Ethereum-based NFTs to register log hashes, LogChain ensures:

- **Immutability**: Once logs are registered, they cannot be altered or deleted.
- **Integrity**: The logs' integrity is ensured using SHA256 hashing algorithms.
- **Traceability**: Every log entry is linked to a unique NFT for complete traceability.

<h2 align="center"> Features</h2>

- **Centralized Log Management**: Aggregates logs from multiple network devices.
- **Secure Log Hashing**: Generates SHA256 hashes for logs and stores them immutably on the blockchain.
- **Blockchain Integration**: Leverages Ethereum blockchain and NFTs (ERC-721) for log registration and integrity.
- **Distributed Storage**: Logs are stored in AWS S3, while their hashes are stored on IPFS and registered on the blockchain.
- **Scalable**: Built on AWS with services like EC2, Lambda, and DynamoDB, ensuring scalability and reliability.

<h2 align="center"> Used Services</h2>

### AWS:
- **EC2**: For running Grafana Loki, which collects and centralizes logs.
- **S3**: Stores log data.
- **DynamoDB**: Stores metadata, including hashes, URLs, and blockchain transaction IDs.![alt text](https://github.com/SLC-ITESO/LogChain/blob/main/DynamoTable.png?raw=true)
- **Lambda**: Handles automation tasks like hashing logs and interacting with IPFS and the blockchain.
- **Elastic Beanstalk**: Hosts the WebApp for querying logs and verifying integrity.

### Blockchain:
- **Ethereum**: Smart contract platform for registering log hashes. Created using EthereumIDE and deploying it in the Sepolia Testnet
- **ERC-721 NFTs**: Used to register each log’s hash as a unique, immutable token.

### Monitoring:
- **Grafana Loki**: Log aggregation, centralization, and querying.

<h2 align="center"> Used Services</h2>

### Logs:
- **Promtail (EC2)**: Used to collect logs to send them to Loki
- **Loki (EC2)**: Centralizes and indexes logs, which are then sent to AWS S3.

### Hashing:
- **Lambda**: Automatically triggered when a new log is uploaded to S3, generating a SHA256 hash for the log(s).

### IPFS + Blockchain:
- Another Lambda function uploads the log's hash to IPFS via Piñata and registers the log’s hash and CID on the Ethereum blockchain.

### Metadata Storage:
- Log metadata, including hash, S3 URL, and CID, is stored in DynamoDB for fast querying.

### WebApp:
- Hosted on Elastic Beanstalk, the WebApp allows users to query logs by hash.

### Validation:
- By comparing the hash from DynamoDB to the hash stored on the blockchain, any tampering or alteration can be detected.

<h2 align="center"> Instances and Functions</h2>

### EC2 Instance:
- **1 EC2 instance** running Loki and Promtail to collect, transform, and monitor logs.

### Lambda Functions:
- **log_to_hash**: Triggered by the upload of logs to S3, this function generates a SHA256 hash and stores it in DynamoDB.
- **hash_to_blockchain**: Registers the generated hash on the Ethereum blockchain and stores the transaction ID in DynamoDB.

<h2 align="center"> Diagram </h2>

![alt text](https://github.com/SLC-ITESO/LogChain/blob/main/LogChainDiagram.png?raw=true)


<h2 align="center"> Results </h2>

Sample of a consult:

![alt text](https://github.com/SLC-ITESO/LogChain/blob/main/LogChainConsult.png?raw=true)

Transaction ID:

![alt text](https://github.com/SLC-ITESO/LogChain/blob/main/Working_TransactionID.png?raw=true)
