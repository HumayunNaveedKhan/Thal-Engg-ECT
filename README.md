# Wireless Modular ECT — Concept Note

**Author:** Hashir · R&D
**Status:** Concept formulation → 2-board prototype
**Scope (this stage):** Continuity testing only

---

## 1. Concept

The Electrical Check Tester is built from **modular 64-point nodes** instead of one
large fixed machine. Each node has its own MCU (ESP32-S3) and talks **wirelessly** to
a central PC. Capacity scales by adding nodes (64 → 128 → …).

- Every pin has a **global address** = `node_id : channel`.
- The harness plugs into the nodes.
- The **central PC** holds the master data and orchestrates the test.

## 2. Key refinement (new)

Continuity is a **relative** measurement — the test current needs a real return path.
Radio can carry the *command* and the *result*, but **not the measurement itself**.

> Therefore all nodes share **one common ground / reference line ("REF spine")** —
> a single thin conductor between boards. Everything else stays fully wireless.

This single detail is what makes the modular wireless approach electrically valid.

## 3. How a test runs

1. PC tells one node: **drive a pin and hold it**.
2. PC tells the target node: **sense** its pin.
3. Node reports the result back wirelessly.
4. PC compares against master data → pass / fail, per pin.

Because the drive is **held steady**, wireless latency/jitter does not affect the
result.

- **Same-board net** → tested locally by that node (fast, no spine needed).
- **Cross-board net** → orchestrated by the PC through the REF spine.

## 4. Two-board prototype spec

| Item | Spec (per board) |
|---|---|
| Test points | 64 switched I/O |
| I/O operating voltage | 24 V |
| Indicators | 64 LEDs (per-pin status) |
| Controller | ESP32-S3, wireless |
| Protection | Opto-isolation on I/O (safeguards the ESP32) |
| Inter-board link | Single shared GND/REF line only — no data cables |
| Central control | Laptop / MacBook over telnet serial (for now) |

## 5. Next steps

- Refine the concept into a robust design.
- Build the two modular boards and demonstrate continuity end-to-end.
- Report progress as it develops.
