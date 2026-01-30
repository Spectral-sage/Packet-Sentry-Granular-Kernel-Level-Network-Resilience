Project Roadmap: Packet-Sentry
This document outlines the development trajectory and technical milestones for Packet-Sentry. Each milestone is designed to ensure a stable, high-performance transition from initial kernel-space hooks to a production-ready network watchdog.

Milestone 1: XDP Ingress Foundation
Objective: Establish the primary enforcement layer at the network driver level.

Tasks:

Implementation of the core XDP C-program for L3/L4 packet parsing.

Development of basic XDP_DROP and XDP_PASS logic based on static IP blacklists.

Setup of the user-space loader using libbpf.

Acceptance Criteria:

Successful line-rate filtering of SYN-flood traffic on x86_64 and ARM64 testbeds.

Measured CPU overhead remains under 1% during a 1Gbps traffic saturation test.

Milestone 2: Stateful eBPF Maps & Anomaly Detection
Objective: Move beyond static filtering to dynamic, stateful threat mitigation.

Tasks:

Implementation of LRU (Least Recently Used) Hash Maps to track per-IP connection states.

Development of kernel-side logic to detect rapid-fire port scanning and rate-limit violations.

Integration of atomic map updates from the user-space control plane.

Acceptance Criteria:

Program successfully passes the BPF Verifier with complex stateful logic.

Automated blocking of IPs exceeding 100 connection attempts per second across multiple ports.

Milestone 3: Low-Overhead Telemetry & Observability
Objective: Provide real-time visibility into kernel-level security events.

Tasks:

Integration of BPF Ring Buffers for asynchronous, non-blocking data export.

Development of a lightweight user-space daemon to consume security events and log them to a JSON-formatted stream.

Creation of a CLI tool to query live eBPF map statistics.

Acceptance Criteria:

Export of 10,000+ security events per second without dropping packets at the kernel ingress.

Zero memory leaks detected in the ring buffer allocation during a 24-hour stress test.

Milestone 4: Cross-Architecture Hardening & Integration
Objective: Ensure portability and ease of deployment for the NGI ecosystem.

Tasks:

Optimization of eBPF bytecode using CO-RE (Compile Once – Run Everywhere) for MIPS and ARM architectures.

Development of a standard configuration schema (UCI/YAML) for integration with OpenWrt and other Linux distributions.

Final performance benchmarking and documentation of hardware-specific optimizations.

Acceptance Criteria:

Successful deployment and functional testing on an OpenWrt-based router.

Complete technical documentation and a "stable" v1.0 release tag on GitHub.