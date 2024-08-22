---
title: "Learn Pub-Sub with ChatGPT"
datePublished: Thu Aug 22 2024 05:04:41 GMT+0000 (Coordinated Universal Time)
cuid: cm04tj8go000e0alb5qjj6am8
slug: learn-pub-sub-with-chatgpt
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/WYd_PkCa1BY/upload/e7fcd1e57949f5d4cf71ad8af9722510.jpeg

---

Publish-Subscribe (Pub/Sub) is a design pattern where objects (subscribers) subscribe to an event or topic and get notified when that event or topic occurs (published) by a publisher. Here's a simple implementation of Pub/Sub in JavaScript:

```javascript
// PubSub object to manage subscriptions and notifications
var PubSub = (function() {
    var topics = {};

    return {
        // Subscribe to a topic
        subscribe: function(topic, listener) {
            // Create the topic if it's not yet created
            if (!topics[topic]) {
                topics[topic] = [];
            }
            // Add the listener to the topic
            topics[topic].push(listener);
        },

        // Publish a message to a topic
        publish: function(topic, data) {
            // If the topic doesn't exist, or there's no listeners in it, just return
            if (!topics[topic] || topics[topic].length === 0) {
                return;
            }
            // Invoke all the listeners in the topic
            topics[topic].forEach(function(listener) {
                listener(data !== undefined ? data : {});
            });
        },

        // Remove a listener from a topic
        unsubscribe: function(topic, listener) {
            if (!topics[topic]) return;
            var index = topics[topic].indexOf(listener);
            if (index !== -1) {
                topics[topic].splice(index, 1);
            }
        }
    };
})();

// Example usage
function onMessageReceived(data) {
    console.log('Message received:', data);
}

PubSub.subscribe('message', onMessageReceived);
PubSub.publish('message', { text: 'Hello, world!' });

// Unsubscribe
PubSub.unsubscribe('message', onMessageReceived);
```

In this implementation:

* The `PubSub` object manages topics and listeners.
    
* `subscribe(topic, listener)` is used to subscribe a listener to a topic.
    
* `publish(topic, data)` is used to publish a message to a topic. All listeners subscribed to that topic will be notified.
    
* `unsubscribe(topic, listener)` is used to remove a listener from a topic.
    

You can use this Pub/Sub implementation to decouple components in your application, allowing them to communicate without having direct references to each other.