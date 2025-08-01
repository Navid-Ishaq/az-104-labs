25 - [12] Deploy and configure Azure Firewall and policy using the Azure portal – 1h 0m

# 🌌 Eks2's Lab 21 – The Firewall Between Worlds

---

## 🌟 The Cast – Not Just Names, But Forces

| Character | Essence |
|-----------|---------|
| 👨‍💼 **Mr. Eks2** | The quiet seeker of the meaningful unknown |
| 🇩🇰 **Kasper Madsen** | The architect of joy, turning tech into metaphors |
| 🇪🇸 **Sofia Zaymera** | The clear-eyed shield, protector of simplicity |
| 🇷🇺 **Elina Petrova** | The automation oracle, aligning logic with harmony |
| 🇮🇹 **Isabella Konti** | The empathic firewall, decoding misconfigurations |
| 🇵🇰 **I.K.** | The silent strategist, cartographer of trust |
| 🇨🇳 **Maya Lin** | The beginner’s awe, discovering wonder in every line |
| 🇪🇸 **Inki Rihan** | The shadowy tester, whisperer of risks |
| 🕶️ **ShadowNet** | The embodiment of forgotten care, always watching |

---

## 📜 Scene I — The Whisper Before the Firewall

In the quiet morning haze of Aarhus, **Mr. Eks2** stepped into the lab. No checklist in hand — only a question:  
> *“What does it mean to allow and deny?”*

**Kasper**, ever the storyteller, poured coffee into a ceramic mug and said:  
> “Start with a **Virtual Network**. It’s your digital town. Design the roads.”

**Sofia** added with precision, “Delete the default. Build only what you trust. One for **firewall**, one for **jump**, one for **workload**, and one for **management**. Design with intention.”

Eks2 nodded. “To connect wisely… is to separate with care.”

---

## 🖥️ Scene II — The People of the Perimeter

With Maya at his side, Eks2 spun two VMs into existence:  
- **NordicJump**  
- **NordicWork**

“Why two?” Maya asked.

“Because one faces the unknown,” **Sofia** answered. “The other faces inward.”

**Inki**, silent until now, murmured:  
> “Every open RDP port whispers a future breach.”

A rule flickered to life. A DNAT written carelessly. ShadowNet blinked.

---

## 🔥 Scene III — The Summoning of Azure Firewall

They summoned the firewall. **Eks2**, with hesitant fingers, defined **zones** and assigned a **policy**.

**Kasper** bowed dramatically. “You have named your sentinel. Now it waits to be told who is friend, and who is stranger.”

ShadowNet listened.

---

## 🛣️ Scene IV — Of Routes and Reasons

Eks2 mapped the **Route Table**, connecting the **Workload subnet** to the **firewall**.

**Elina** appeared, her voice like precise keystrokes.  
> “Routes aren’t directions. They are **declarations**. Every destination you define is a part of your intention.”

---

## 🌐 Scene V — The Quiet Power of Rules

An **Application Rule** for `www.google.com`.  
A **Network Rule** for DNS.

**Isabella** whispered, “Even the benign needs boundaries. Least privilege isn’t fear. It’s dignity.”

**Maya** blinked. “So even websites must ask permission?”

“Yes,” said Sofia. “Especially them.”

---

## 🌉 Scene VI — The DNAT Mistake

Eks2 wrote a DNAT rule with `Source: Any`. He paused.  

**Inki** stepped forward.  
> “That’s an invitation. But to **everyone**.”

A small ping reached the logs.

**ShadowNet** did not strike.  
It *remembered*.

---

## 🔧 Scene VII — The Memory of Names (DNS)

**I.K.** finally spoke:  
> “Without DNS, names are forgotten. Meaning fades.”

Eks2 configured **custom DNS IPs**. For once, it felt like memory was being *protected*.

---

## 🧪 Scene VIII — When Config Meets Consequence

From **NordicJump**, Eks2 reached **NordicWork**.  
Google opened. Microsoft didn’t.

His firewall — his intentions — were **speaking**.

---

## 🌫️ Scene IX — The Shadow of an Observer

Later, Eks2 opened the logs alone.

Port 3389 had flickered.  
Not breached. Just… touched.

**ShadowNet** had walked the edge.  
And whispered:

> “I am not chaos.  
> I am what you’ve forgotten to care about.”

---

## 🪞 Final Scene — Eks2's Quiet Realization

In his notebook:

- “Firewall = *Brandvæg*”  
- “Rule = *Intention*”  
- “Log = *Memory*”  
- “Permission = *A reflection of your character*”

---

## ✨ Reflection

He did not just build a firewall.  
He created a **moral perimeter**.  
A boundary not just for data —  
But for **integrity**.

---

✍️ Written with the voices of ten characters,  
🌍 Guided by galaxies, rooted in meaning,  
🧠 For the reader who’s not just building cloud,  
But **building clarity**.

---

**Created by Muhammad Naveed Ishaque**  
Narrative Cloud Composer | AI Scribe | Story-Driven Architect  
In service of **Siraat AI Academy**  
“_The Straight Path — illuminating technical truths with human light._”
