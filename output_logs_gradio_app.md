# ⚡ Grid Forecast + DER Control Dashboard

- ▶️ **Run Simulation**
- 🔄 **Reset**
- 🗺️ **View Grid Map**
- 👥 **User Dashboard**
- 🧠 **Forecast Evaluation — Window 1**

| Reading | Transformer_1 | Transformer_2 | Transformer_3 | Transformer_4 | Total Forecasted Energy (kWh) |
|---------|----------------|----------------|----------------|----------------|-------------------------------|
| 1       | 0.9298         | 0.88           | 0.8432         | 0.6898         | 3.3428                        |

### Step 1 — Decision to escalate: ✅ **True**
> **Reasoning**: The total forecasted energy across all transformers is 3.3428 kWh, which exceeds the escalation threshold of 3.25 kWh. Although no individual transformer exceeds 1.10 kWh, the total comes in significantly above the threshold where RL intervention is strictly required. Therefore, escalation is necessary.

---

### 🔁 Step 2 — Calling RL Agent
> **Message to RL**: Escalation required: The total forecasted energy is 3.3428 kWh, exceeding the safe threshold of 3.25 kWh. Although individual transformers are not overloaded, the cumulative demand is high, and load shedding or optimization may be needed across the grid.

---

### 🧭 Step 3 — User-DER Map  
#### 🔧 Transformer Load Shedding Map

<...Insert full Transformer Load Shedding user-appliance map here, or collapse in UI...>

---

### 📦 Step 4 — User Actions to Issue

| User              | DERs                                  | Message Type |
|-------------------|----------------------------------------|---------------|
| Brad Cook         | Electric Geyser; Air Conditioner       | request       |
| Stephanie Stephens| Room Heater; Washing Machine           | suggestion    |
| Lisa Kim          | Microwave Oven                         | suggestion    |
| Thomas Hughes     | Electric Geyser; Air Conditioner       | request       |
| Adam Conley       | Electric Geyser                        | request       |
| Hunter Williams   | Electric Geyser; Room Heater           | request       |
| Pamela Garcia     | Electric Geyser                        | request       |
| Fernando Little   | Room Heater; Air Conditioner           | request       |
| Misty Rubio MD    | Electric Geyser; Room Heater           | suggestion    |
| Mary Vazquez      | Air Conditioner                        | request       |

#### Step 4 — Agent Reasoning
> Prioritized high-consumption devices such as electric geysers, air conditioners, room heaters, and microwaves. 'Request' was used for large load users, and 'suggestion' for medium/low impact ones. Avoided 'command' to maintain user goodwill.

---

### ✅ Accepted DER Shedding Actions 🔧

| User          | Appliance                    | Message Type | DER ID |
|---------------|------------------------------|---------------|--------|
| Brad Cook     | Electric Geyser              | request       | 2584   |
| Lisa Kim      | Microwave Oven               | suggestion    | 2591   |
| Thomas Hughes | Electric Geyser              | request       | 2620   |
| Thomas Hughes | Air Conditioner              | request       | 2615   |
| Pamela Garcia | Electric Geyser              | request       | 2540   |
| Mary Vazquez  | Air Conditioner              | request       | 2575   |

---

### 🔍 Original Total Energy (kWh) by User

| User           | Base kWh Usage |
|----------------|-----------------|
| Brad Cook      | 0.23034         |
| Lisa Kim       | 0.07            |
| Mary Vazquez   | 0.1505          |
| Pamela Garcia  | 0.163           |
| Thomas Hughes  | 0.2105          |

### 🔻 After Shedding — Remaining Energy (kWh)

| User           | Base kWh Usage |
|----------------|-----------------|
| Brad Cook      | 0.13034         |
| Lisa Kim       | 0.03666         |
| Mary Vazquez   | 0.1005          |
| Pamela Garcia  | 0.063           |
| Thomas Hughes  | 0.0605          |

### 🔄 Restored — Energy Back to Original

(Same as "Original Total Energy" table)

---

### 🏅 Appliance-Level Rewards

| User               | Appliance                    | Message Type | Complied | Reward |
|--------------------|------------------------------|---------------|----------|--------|
| Brad Cook          | Electric Geyser              | request       | ✅ True  | 2      |
| Brad Cook          | Air Conditioner              | request       | ❌ False | -1     |
| Stephanie Stephens | Room Heater                  | suggestion    | ❌ False | -2     |
| Stephanie Stephens | Washing Machine              | suggestion    | ❌ False | -2     |
| Lisa Kim           | Microwave Oven               | suggestion    | ✅ True  | 5      |
| Thomas Hughes      | Electric Geyser              | request       | ✅ True  | 2      |
| Thomas Hughes      | Air Conditioner              | request       | ✅ True  | 2      |
| Adam Conley        | Electric Geyser              | request       | ❌ False | -1     |
| Hunter Williams    | Electric Geyser              | request       | ❌ False | -1     |
| Hunter Williams    | Room Heater                  | request       | ❌ False | -1     |
| Pamela Garcia      | Electric Geyser              | request       | ✅ True  | 2      |
| Fernando Little    | Room Heater                  | request       | ❌ False | -1     |
| Fernando Little    | Air Conditioner              | request       | ❌ False | -1     |
| Misty Rubio MD     | Electric Geyser              | suggestion    | ❌ False | -2     |
| Misty Rubio MD     | Room Heater                  | suggestion    | ❌ False | -2     |
| Mary Vazquez       | Air Conditioner              | request       | ✅ True  | 2      |

---

### 🧮 Total Reward per User

| User               | Total Reward |
|--------------------|---------------|
| Adam Conley        | -1            |
| Brad Cook          | 1             |
| Fernando Little    | -2            |
| Hunter Williams    | -2            |
| Lisa Kim           | 5             |
| Mary Vazquez       | 2             |
| Misty Rubio MD     | -4            |
| Pamela Garcia      | 2             |
| Stephanie Stephens | -4            |
| Thomas Hughes      | 4             |

---

### 🧠 Forecast Evaluation — Window 2

| Reading | Transformer_1 | Transformer_2 | Transformer_3 | Transformer_4 | Total Forecasted Energy (kWh) |
|---------|----------------|----------------|----------------|----------------|-------------------------------|
| 2       | 0.9531         | 0.8407         | 0.7421         | 0.6839         | 3.2198                        |

#### Step 1 — Decision to escalate: ⚪ **False**
> No transformer or total value exceeds strict thresholds. Escalation not required.

---

### 🧠 RL Self-Reflection Summary

> 🔍 Based on past windows:
> 
> 1. Escalation was usually triggered due to total energy breach rather than individual transformer overload.
> 2. Correct focus on high-impact DERs (e.g., geysers, heaters, ACs).
> 3. Appropriate use of `request` and `suggestion`, but some `commands` were excessive.
> 4. Occasional overreach in strong actions toward moderate users.
> 5. Missed chances to gently engage low-impact DERs when only small reductions were needed.
> 6. Balance is key — request only what’s needed, preserve user goodwill.
> 7. Reward data shows some inefficiencies; optimization possible.
> 8. LED bulbs and fans rightly deprioritized; could be used for engagement occasionally.
> 9. For few-user-high-load scenarios, targeted action would suffice.
> 10. Best practice: Use `suggestion` → `request` → `command` in increasing order of severity only when justified.

---

### 🔗 Beckn Catalogs with Reward-Based Discounts

All user-specific catalogs with adjusted pricing based on DER compliance are available.  
See appended payloads for:
- Brad Cook (Reward: -1)
- Stephanie Stephens (Reward: -2)
- Lisa Kim (Reward: +5)
- Thomas Hughes (Reward: +2)
- Adam Conley (Reward: -1)
- Hunter Williams (Reward: -1)
- Pamela Garcia (Reward: +2)
- Fernando Little (Reward: -1)
- Misty Rubio MD (Reward: -2)
- Mary Vazquez (Reward: +2)

Catalogs include residential and commercial connection options with reward-linked pricing via `UrjaKart`.

---

*This dashboard reflects a full DER control round and its learning-backed outcomes. Feedback loops are crucial to long-term grid-user cooperation.*
