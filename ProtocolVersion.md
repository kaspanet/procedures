# Kaspa: Protocol Version

This document describes how the kaspa protocol is versioned and used.

**Refers** [procedures/Versioning.md](https://github.com/kaspanet/procedures/blob/master/Versioning.md).

---
#### TL; DR
* *Kaspa protocol version* is derived from the *kaspad version* it was firstly introduced on.
* It is *encoded* as a `uint32` with one byte per version-element and a reserved 0 byte (e.g. **3.11.26** is **0x030b1a00**).
* When two peers connect, the newer one should decide if the other's version is compatible with its own.
---

## Meaning
The *kaspa protocol version* defines the version of the protocol used in the kaspa p2p-network. It is different than *kaspad version*, that is, the version of the code itself. 

## Assigning
By convention and for the sake of simplicity, the *protocol version* will be derived from the version of the *kaspad* code. That means, when a protocol change is being introduced, its version should be set according to the current *kaspad* version.

#### Examples
If a new *kaspad version* **3.7.2** is released, that introduces a change in the protocol, then the new protocol version will be **3.7.2** as well.
If a new *kaspad version* is released later as **3.8.0**, that contains no change to the protocol, then it will still use *protocol version* **3.7.2**.

## Encoding
The *encoded form* of the version is its representation within peer-to-peer message.  The version is encoded as a `uint32` number, where -
* The first byte represents the major version part
* The second byte represents the minor version part
* The third byte represents the revision version part
* The fourth byte is reserved and should usually be set to 0

#### Examples
Version **3.2.7** is encoded as **0x 03 02 07 00**.
Version **3.11.26** is encoded as **0x 03 0b 1a 00**.

## Ordering
Using this encoding, given two versions **x.y.z** and **a.b.c**, the first is newer (higher) than the latter iff the encoded version of the first is higher than the encoded version of the latter, assuming network (big) endianess.

#### Examples
Referring to the two versions above - the relation between the versions is
**3.2.7 < 3.11.26**, 
and in the same way, the relation between their encoded forms is
**0x03020700 < 0x030b1a00**.

## Compatibility
When two peers connect, they should provide their *protocol versions* to each other. It is the responsibility of the node that uses a newer (higher) version to decide whether they are compatible or otherwise reject the connection.
