# Getting Started

AnyCable acts like a bridge beetween _logic-less_ WebSocket server and _Action Cable-like_ Ruby framework (i.e. framework which support [Action Cable protocol](./action_cable_protocol.md)).

<div class="chart-container">
  <img src="./assets/images/anycable.svg" alt="AnyCable diagram" width="40%">
</div>

The main goal of AnyCable is to make it possible to write high-performant real-time application using Ruby as a language for implementing a business-logic.

This goal is achieved by _moving_ low-level responsibility (handling sockets, parsing frames, broadcasting data) to WebSocket servers written in other languages (such as Golang or Erlang).

AnyCable could be used with the existing Action Cable clients (such as [JavaScript client](https://www.npmjs.com/package/actioncable) or [Action Cable CLI](https://github.com/palkan/acli)) without any change.

You can use AnyCable with:
- Action Cable (Rails) apps (see [Using with Rails](./using_with_rails.md))
- [Lite Cable](./lite_cable.md) for  _plain_ Ruby projects (see [Using with Ruby](./using_with_ruby.md))
- your own [AnyCable-compatible framework](./how_to_anycable_framework.md).

As a WebSocket server you can choose:
- [`anycable-go`](./anycable_go.md) (Golang) (_recommended_)
- [`erlycable`](./erlucable.md) (Erlang)
- your own [AnyCable-compatible server](./how_to_anycable_server.md)