# Overview

| Feature        | Long Polling                                                              | Server-Sent Events (SSE)             | WebSockets                      |
| -------------- | ------------------------------------------------------------------------- | ------------------------------------ | ------------------------------- |
| Direction      | Client → Server → Client                                                  | Server → Client only                 | Client ↔ Server (full-duplex)   |
| Transport      | HTTP requests                                                             | HTTP streaming (`text/event-stream`) | WebSocket protocol (upgrade)    |
| Message Format | Any (JSON, text)                                                          | Text (UTF-8 only)                    | Text + Binary                   |
| Latency        | Medium                                                                    | Low                                  | Very low                        |
| Overhead       | High (repeated requests); server needs to manage lots of open connections | Low (single connection)              | Very low (persistent socket)    |
| Complexity     | Simple                                                                    | Simple                               | More complex                    |
| Auto Reconnect | Client-managed                                                            | Built-in                             | Must implement manually         |
| Use Cases      | Legacy browsers, simple updates                                           | Notifications, feeds, dashboards     | Chat, games, collaborative apps |

# Sever Sent Events
 - plain HTTP over TCP (single long-lived http connection)
 - One Way: Server -> Client
 - Response Header
	 - Content-Type: text/event-stream
	 - Cache-Control: no-cache
	 - Connection: keep-alive
 - Client creates an EventSource object (automatic reconnection)
	 - const evtSource = EventSource("/events")
	 - evtSource.onmessage = () => {}

# Websocket

## Server

## Client
