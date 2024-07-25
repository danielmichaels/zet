# RabbitMQ missed heartbeat BlockingConsumer

Fix missed heartbeats from client, add the following line of code:

    connection.process_data_events()

This is for when using a `basic_consume`, `start_consuming`.

ref: https://anands.me/blog/pika-missed-heartbeats-rabbitmq
