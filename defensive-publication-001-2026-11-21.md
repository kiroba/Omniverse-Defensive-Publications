# Defensive Publication No. 1 — Omniverse Mesh Mechanisms

**Author:** Kiro (Hactik Games Studios)
**Date of publication:** November 21, 2026
**Purpose:** This document is published deliberately, in enabling detail, to establish prior art. The mechanisms described below are dedicated to the public as prior art so that they remain available to all implementers and cannot later be claimed exclusively by any party. This publication is not a patent application and asserts no exclusive rights.

The Omniverse is a decentralized, local-first mesh ecosystem: applications (Flutter/Dart) and a per-device daemon (Python stdlib) communicate through signed event envelopes relayed between phones and always-on nodes, with no central server.

---

## 1. Envelope encryption arrangement for mesh applications and their daemon

A storage-encryption arrangement for a system split between mobile applications and a local daemon:

- Data is encrypted with a per-store data encryption key (DEK). The DEK is held in platform secure storage (e.g., Android Keystore-backed secure storage) on the application side.
- The encrypted store is a SQLCipher database. In a first version, only the event payload column (`events.payload_json`) is encrypted; event metadata (ids, timestamps, authors, hashes) remains plaintext by design, so relay, indexing, and sync operate without decryption.
- On the daemon side, the key root is an **operator passphrase**, stretched with scrypt. The stretched key wraps both the DEK and the node's own Ed25519 signing key, replacing storage of the node key as a raw plaintext file protected only by filesystem permissions.
- A standing design rule accompanies the arrangement: **no field belonging to a user's private data layer may ever be stored in the event store or in an event payload in plaintext**, in any component, regardless of the encryption version in force.

## 2. Containment enclaves: sanction by enclosure rather than exile

A moderation mechanism for a decentralized network in which a sanctioned participant is not removed from the network but is placed in a **private jailed enclave**:

- A three-state ladder applies: full standing → limited standing → contained (jailed enclave). A further severed tier exists for conduct that breaks real-world law: no mesh membership at all, connection possible only by a peer's explicit add, and that link remains limited indefinitely.
- A contained participant keeps their own data, identity, and local use of their own device and creations. What is restricted is their reach into the shared network.
- Sanctions are legitimized by signed public broadcasts and enforced by peers, not by a central authority. Minors are entirely excluded from the containment system.
- The record of a sanction persists permanently, but evidentiary and personal detail is **sealed after release** from containment; the fact of the record remains, the detail does not remain public.
- False or abusive sanction proposals are themselves gradeable conduct: the proposer's reputation takes the hit, with no separate staking mechanism.

## 3. Behavioral echoes constrained to a public persona

A system of software presences ("Echoes") representing a person in shared virtual spaces they are not currently occupying:

- Each Echo is generated from a single **owner-issued signed package** containing a personality description, a set of facts the owner allows the Echo to use, and a behavior version. The same package is used in every space, so the Echo is the same character everywhere.
- An Echo is constructed **only from the person's public persona layer**. It never accesses, carries, or reveals data from the person's private layer, which is never relayed.
- An Echo does not sign or post as the person except where the owner has explicitly enabled signing, and any such action follows a standing flow of alerts, warnings, and risk notifications to the owner.
- Meeting an Echo does not register a relationship with its owner; a meeting exchanges only name, identity hash, and location met, and ticks a people-met counter.
- Presence follows a visitation pattern: an Echo of a person met once visits for a few days of real time and then stops unless the parties meet again; Echoes of friends keep visiting. When the real person enters a space, their Echo vanishes and merges into the person for the duration, and visits restart when the person leaves.

## 4. Proximity bootstrap, sealed relay, and hash-addressed asset distribution

A bootstrap and distribution arrangement for a phone-and-node mesh:

- Two phones establish identity exchange by a **Bluetooth Low Energy introduction**: in physical proximity, the phones discover each other, exchange signed identity material and profile events, and record sighting reports, bootstrapping a relationship that later continues over IP.
- Relay is performed by any reachable node acting as rendezvous or relay. Relays carry **sealed, signed event envelopes they cannot read**; no single node is special or irreplaceable, and any node can play either role.
- Content distribution is **hash-addressed and deduplicated**: content is identified and verified by its hash, streamed from nodes rather than stored whole at every destination, and the same content under the same hash is stored once and shared by reference, with the limited copies placed deliberately where they are useful.

## 5. Signed skill packs with witnessed progression, and roaming agents

A learning system for software agents ("Halos") attached to a person:

- Skills are distributed as **signed skill packs** containing four component types: TEACH (instruction), ROUTINE (a repeatable procedure), PRACTICE (exercises), and WITNESS (attestation requirements).
- Experience points (XP) unlock a pack, but progression through the states **Learning → Practiced → Trusted** advances **only on witnessed practice** — practice attested by another participant or node — never on self-report alone.
- A Halo may **roam the network unattended**, travelling node-to-node and phone-to-phone while its owner is absent, encountering items, discoveries, and other agents. Roaming earns XP at a multiplied rate (1.5x–2x over local activity), the multiplier climbing with unattended time and weighted by finds and reputation. Earned XP is exchangeable for skills.
- Roaming is bounded by owner-set roam limits, and roam access points are kiosks (in-world or in-app) entered with an identifier string.

---

*End of Defensive Publication No. 1.*
