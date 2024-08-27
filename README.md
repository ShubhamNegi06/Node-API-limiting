# Node-API-limiting
=====================
# Node.js API with Rate Limiting and Clustering

This project demonstrates how to build a Node.js API with rate limiting and task queuing. The API is set up with clustering using PM2 to handle high loads and ensure tasks are processed according to specified rate limits.

## Features

- **Rate Limiting:** Limits requests to 1 task per second and 20 tasks per minute per user ID.
- **Task Queuing:** Tasks are processed in a queue, respecting the rate limits.
- **Clustering:** Utilizes PM2 to manage multiple instances of the API server for load balancing.

## Setup

### 1. Set Up Node.js API

1. **Initialize the Node.js Project:**

    ```bash
    mkdir rate-limiting-api
    cd rate-limiting-api
    npm init -y
    ```

2. **Install Dependencies:**

    ```bash
    npm install express redis rate-limiter-flexible
    ```

    - `express` for building the API.
    - `redis` for in-memory data storage.
    - `rate-limiter-flexible` for handling rate limiting.

3. **Create `server.js` File:**

### 2. Set Up Clustering with Two Replicas

1. **Install PM2 for Clustering:**

    ```bash
    npm install -g pm2
    ```

2. **Start the Cluster:**

    ```bash
    pm2 start server.js -i 2
    ```

    The `-i 2` flag tells PM2 to run 2 instances of your API server.

3. **Check PM2 Status:**

    ```bash
    pm2 status
    ```

    This will show you the status of your clusters and ensure they're running.

### 3. Test the API

1. **Test the Rate Limiting and Queuing:**

    Use tools like Postman or curl to send requests to your API. Make sure to include the `user-id` in the headers and observe the rate limiting behavior.

    ```bash
    curl -X POST http://localhost:3000/task -H "Content-Type: application/json" -H "user-id: test-user" -d '{"task": "example"}'
    ```

2. **Monitor Logs and Performance:**

    Monitor the logs using PM2 to check for any errors or issues with task processing.

    ```bash
    pm2 logs
    ```

## Notes

- Ensure Redis is running and accessible.
- Adjust the rate limit settings as needed for your application.
- Modify the task processing logic according to your needs.

This setup ensures that tasks are processed according to the specified rate limits for each user ID, using an in-memory queue and Redis for rate limiting. Adjust the configuration and handling as necessary based on your specific requirements and environment.

