# noesis-ship

[![Crates.io](https://img.shields.io/crates/v/noesis-ship.svg)](https://crates.io/crates/noesis-ship)
[![Documentation](https://docs.rs/noesis-ship/badge.svg)](https://docs.rs/noesis-ship)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Rust NATS communication platform for multi-agent AI systems.

## Features

**Five core primitives** over [NATS](https://nats.io):

| Primitive | Transport | Use Case |
|-----------|-----------|----------|
| **PubSub** | NATS Core | Fire-and-forget broadcast |
| **EventBus** | JetStream | Durable event streaming with replay |
| **Channels** | JetStream | Point-to-point messaging with history |
| **KV Store** | NATS KV | Shared state (registry, config, health) |
| **Object Store** | NATS Object Store | Large blob storage with SHA-256 |

Plus **NatsServiceBuilder** — build a NATS request-reply service in ~20 lines:

```rust
use noesis_ship::service::NatsServiceBuilder;

NatsServiceBuilder::new("myservice.cmd", MyState::default())
    .nats_url("nats://localhost:4222")
    .handler("echo", |payload, _state| payload.to_vec())
    .run()
    .await?;
```

## Quick Start

```rust
use noesis_ship::connection::ConnectionManager;
use noesis_ship::types::NatsConfig;

let config = NatsConfig::new("nats://localhost:4222");
let mut conn = ConnectionManager::new(config);
conn.connect().await?;
```

## Requirements

- Rust 1.85+ (edition 2024)
- NATS server 2.10+ (with JetStream enabled)

## License

MIT — Copyright (c) Hank Head / Congruent Systems PBC
