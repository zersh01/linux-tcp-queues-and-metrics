# Linux TCP Queues and Metrics

Detailed diagram of the Linux TCP stack: incoming & outgoing connections, queues (SYN, Accept, backlog), drops, TcpExt metrics, netfilter hooks, conntrack, and tuning points.

![Linux TCP Stack Diagram — Incoming / Outgoing, Queues, TcpExt Metrics](images/tcp-stack-en.svg)  

## Key Parts Covered
- Incoming path: NIC → RX Ring → Netfilter PREROUTING/INPUT → SYN Queue → Accept Queue → Application
- Outgoing path: Application → TX → Netfilter OUTPUT/POSTROUTING → NIC
- Queues & bottlenecks: netdev_max_backlog, tcp_max_syn_backlog, somaxconn, conntrack overflow
- TcpExt metrics: ListenDrops, ListenOverflows, TCPBacklogDrop, ExtStats, etc.
- Common issues: retransmits, memory pressure, delayed ACK, TFO, SACK, PAWS

Ideal for debugging and tuning high-load TCP servers (Nginx, HAProxy, etc.).

## License
Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)

## Author
zersh01[](https://github.com/zersh01)
