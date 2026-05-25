# Day 20 - Spanning Tree Protocol (STP) Part 1
> 📺 Jeremy's IT Lab | CCNA 200-301 Complete Course

---

## 📌 What is STP?

- **Spanning Tree Protocol (STP)** is a Layer 2 protocol defined in **IEEE 802.1D**
- It **prevents Layer 2 loops** in networks with redundant paths
- Without STP, broadcast frames would loop forever → **broadcast storm**
- STP **blocks** redundant ports to create a loop-free logical topology

---

## ⚠️ Why Layer 2 Loops Are Dangerous

| Problem | Description |
|---|---|
| **Broadcast Storm** | Broadcasts loop endlessly, consuming all bandwidth |
| **MAC Table Instability** | Switches keep updating MAC tables with conflicting info |
| **Multiple Frame Copies** | Devices receive duplicate frames |

> 💡 Unlike Layer 3, there is **no TTL** at Layer 2 — frames loop forever!

---

## 🔁 How STP Works (Overview)

1. Elect a **Root Bridge**
2. Each non-root switch selects its **Root Port** (best path to Root Bridge)
3. Each network segment selects a **Designated Port**
4. All other ports become **Non-Designated (Blocked)**

---

## 🏆 Step 1 — Root Bridge Election

- All switches send **BPDUs (Bridge Protocol Data Units)** out all ports
- The switch with the **lowest Bridge ID** becomes the Root Bridge
- **All ports on the Root Bridge are Designated Ports (Forwarding)**

### Bridge ID Structure (8 bytes total)

```
[ Bridge Priority (4 bits) | VLAN ID (12 bits) ] + [ MAC Address (6 bytes) ]
```

| Field | Size | Default |
|---|---|---|
| Bridge Priority | 4 bits | **32768** |
| Extended System ID (VLAN) | 12 bits | VLAN number |
| MAC Address | 6 bytes | Lowest wins |

> 🔑 Priority must be set in **multiples of 4096** (0, 4096, 8192 ... 61440)

**Tiebreaker order:**
1. Lowest **Bridge Priority** wins
2. If tie → Lowest **MAC Address** wins

---

## 🛤️ Step 2 — Root Port Selection (Non-Root Switches)

Each non-root switch picks **one Root Port** — the port with the **lowest root cost**.

### STP Port Costs (Classic 802.1D)

| Speed | STP Cost |
|---|---|
| 10 Mbps | 100 |
| 100 Mbps | 19 |
| 1 Gbps | 4 |
| 10 Gbps | 2 |

**Tiebreaker order (if costs are equal):**
1. Lowest **neighbour Bridge ID**
2. Lowest **neighbour Port ID** (priority + port number)
3. Lowest **local Port ID**

---

## 🔌 Step 3 — Designated Port Selection

- On every network **segment (collision domain)**, one port must be **Designated (Forwarding)**
- The switch with the **lowest root cost** on that segment wins the Designated Port
- If costs tie → **lowest Bridge ID** wins

> ✅ Root Bridge ports = always Designated
> ✅ Root Ports = always Forwarding
> ❌ Non-Designated Ports = **Blocking**

---

## 📦 BPDU (Bridge Protocol Data Unit)

- Sent every **2 seconds** (Hello Timer)
- Contains: Root Bridge ID, Root Path Cost, Sender Bridge ID, Port ID
- Only the **Root Bridge** originates BPDUs; others **relay** them

---

## 🚦 STP Port States

| State | Send/Receive BPDUs | Learn MACs | Forward Frames |
|---|---|---|---|
| **Blocking** | Receive only | ❌ | ❌ |
| **Listening** | ✅ | ❌ | ❌ |
| **Learning** | ✅ | ✅ | ❌ |
| **Forwarding** | ✅ | ✅ | ✅ |
| **Disabled** | ❌ | ❌ | ❌ |

### STP Timers

| Timer | Default | Purpose |
|---|---|---|
| Hello | 2 sec | How often Root sends BPDUs |
| Forward Delay | 15 sec | Time spent in Listening & Learning each |
| Max Age | 20 sec | How long to wait before changing topology |

> ⏱️ Total convergence time: **~50 seconds** (20 + 15 + 15)

---

## 🖥️ Useful IOS Commands

```bash
# Show STP status for all VLANs
show spanning-tree

# Show STP for a specific VLAN
show spanning-tree vlan 1

# Set switch as primary root bridge
spanning-tree vlan 1 root primary

# Set switch as secondary root bridge
spanning-tree vlan 1 root secondary

# Manually set bridge priority
spanning-tree vlan 1 priority 4096

# Set port cost manually
spanning-tree vlan 1 cost 10

# Set port priority
spanning-tree vlan 1 port-priority 64
```

---

## 🧠 Key Terms to Remember

| Term | Meaning |
|---|---|
| **BPDU** | Bridge Protocol Data Unit — STP messages |
| **Root Bridge** | Switch with lowest Bridge ID; central reference point |
| **Root Port** | Best port toward the Root Bridge (one per switch) |
| **Designated Port** | Forwarding port on each segment |
| **Non-Designated Port** | Blocking port — prevents loops |
| **Bridge ID** | Priority + MAC Address |
| **Path Cost** | Cumulative cost of links to Root Bridge |

---

## ✅ Summary

```
Root Bridge      → Lowest Bridge ID (Priority + MAC)
Root Port        → Lowest cost path to Root Bridge (one per non-root switch)
Designated Port  → One per segment; lowest cost to Root Bridge
Blocking Port    → All others; prevents loops
```

---

*📖 Next: Day 21 — Spanning Tree Protocol Part 2 (Port Fast, BPDU Guard, STP Toolkit)*
