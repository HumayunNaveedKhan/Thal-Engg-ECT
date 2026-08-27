# Indigenous Wireless Electrical Check Tester (ECT / OMI)

[![Hardware License](https://img.shields.io/badge/Hardware-CERN--OHL--S-blue.svg)](https://cern.ch/cern-ohl)
[![Firmware License](https://img.shields.io/badge/Firmware-MIT-green.svg)](LICENSE)
[![Standard Compliance](https://img.shields.io/badge/Standards-IATF%2016949%20%7C%20IPC--WHMA--A--620-orange.svg)](#standards-compliance--qa)
[![Build Status](https://img.shields.io/badge/Status-Phase%201%20Validated-brightgreen.svg)](#project-roadmap)

An industrial-grade, modular, 4-wire Kelvin Electrical Check Tester (ECT / OMI) designed for 100% end-of-line verification of automotive and industrial wire harnesses. Built with zero single-supplier dependencies, utilizing standard off-the-shelf solid-state opto-isolated switching and precision Delta-Sigma analog measurement.

---

## 1. Executive Summary & Vision

In automotive wire harness manufacturing, passing a defective harness downstream to an OEM assembly plant results in severe line-stoppage penalties, warranty recalls, and safety hazards. Standard manual multimeter continuity checks cannot guarantee the zero-defect standard required by Tier-1 suppliers.

Commercial automotive harness testers (Cirris, NAC Man, CableEye, Weetech) cost between **$8,000 and $30,000 USD** and rely on closed-source, proprietary expansion hardware.

This project delivers an **open, auditable, high-reliability 512-to-1024 point tester** that can be manufactured turnkey through standard PCB assemblers for under **$700 USD**, providing:
* **Zero False-Accept Guarantee:** True 4-Wire Kelvin sensing completely eliminates switch $R_{ON}$ drift, detecting high-resistance crimps down to milliohms.
* **Rapid Group Isolation:** Matrix scanning algorithm completes 512-point harness checks (continuity + isolation) in **under 1.5 seconds**.
* **Total Local Sourcing Independence:** Designed strictly around components with multiple cross-manufacturer footprints (SOP-4 PhotoMOS, SOIC-20 Power Shift Registers, standard TI ADCs).

---

## 2. Core Measurement Principles

### 2.1 The 4-Wire Kelvin Architecture

In conventional 2-wire testing, the switch on-resistance ($R_{ON} \approx 0.5\ \Omega - 4\ \Omega$) and internal fixture wiring add directly to the measured resistance:
$$R_{\text{measured}} = R_{\text{crimp1}} + R_{\text{wire}} + R_{\text{crimp2}} + 2 R_{\text{switch}} + R_{\text{fixture}}$$

Because a bad crimp is typically defined as any contact resistance exceeding $1.0\ \Omega$, 2-wire testing cannot distinguish between a loose crimp and switch resistance variance.
