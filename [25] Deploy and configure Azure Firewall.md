25 - [12] Deploy and configure Azure Firewall and policy using the Azure portal – 1h 0m


# ✨ Eks2's “Lab to Soulful Story” – Lab 21: Creating Azure Firewall 🌸

---

## 🌟 Meet the Minds Behind the Mission

| Character | Role |
|-----------|------|
| 👨‍💼 **Mr. Eks2** | The whisper of curiosity, discovering cloud wisdom one step at a time in Denmark |
| 🇩🇰 **Kasper Madsen** | The joyful Azure expert who simplifies tech with coffee-laced metaphors |
| 🇪🇸 **Sofia Zaymera** | The calm guardian of clarity, guiding others with simplicity and security grace |
| 🇷🇺 **Elina Petrova** | The automation genius, turning complexity into IaC harmony |
| 🇮🇹 **Isabella Konti** | The empathic firewall who sees the human behind every misconfiguration |
| 🇵🇰 **I.K.** | The unseen spiritual strategist who connects security to meaning and trust |
| 🇨🇳 **Maya Lin** | The fearless rookie, learning with wonder and awe at every turn |
| 🇪🇸 **Inki Rihan** | The phantom Red Teamer, revealing what hides in misused permissions |
| 🕶️ **ShadowNet** | The silent presence of risk — born not of malice, but of forgotten care |

---

## 📖 The Story: Lab 21 — A Firewall Rises

---

### ☁️ Scene 1: The Cloud Village Begins

The morning mist rolled over the Siraat AI Campus in Aarhus as **Mr. Eks2** entered the lab pod. A new mission awaited him — today, he would **build a virtual perimeter**. His hands trembled gently with the weight of possibility.

**Kasper** handed him a coffee. “You ready to design your first digital town, Eks2? Start with the **Virtual Network** — it’s like drawing roads and assigning districts.”

**Sofia** added, “Delete the default subnet. Create only what is needed: one for the **firewall**, one for the **jump box**, one for the **workload**, and a secure **management subnet**.”

> “So I design not just connections,” Eks2 whispered, “but separations.”

**I.K.**, somewhere nearby, nodded in silence.

---

### 🖥️ Scene 2: Citizens of the Network — Two Virtual Machines

**Maya** beamed as **Eks2** created two **VMs** — one he named *NordicJump*, the other *NordicWork*.

**“Why two?”** she asked innocently.

**Sofia** explained: “*Jump* is the bridge. It faces the edge. *Work* is deeper — hidden, protected. Only accessible through trusted hands.”

**Inki Rihan**’s voice floated in softly, “But if RDP stays open to the world, *trust becomes exposure*.”

A flicker passed over the terminal. A port rule was added. A rule too open.

---

### 🔥 Scene 3: The Azure Firewall Awakens

**Eks2** followed the steps carefully — creating the **Firewall**, assigning a **policy**, defining **zones**.

**Kasper** smiled, “You’ve just summoned a guardian. Now teach it who may enter — and who must wait.”

In the distance, **ShadowNet** stirred.

Its eyes flicked toward the open DNAT rule being written.

---

### 🛣️ Scene 4: The Roads of Direction

Creating the **Route Table**, **Eks2** connected the **Workload subnet** to the **firewall**.

**Elina** entered the room, boots clicking with automation rhythm. “Make sure your traffic obeys the road signs,” she said. “In code, every rule has a reason. And every route, a purpose.”

---

### 🌐 Scene 5: Application & Network Rules

**Eks2** wrote an **Application Rule** for `www.google.com`, a **Network Rule** for DNS.

**Isabella** leaned over his shoulder. “Be careful. The more you allow, the more they expect. Least privilege isn’t paranoia. It’s respect.”

**Maya** asked, “So... even websites need permission?”

**Sofia** nodded. “Especially them.”

---

### 🌉 Scene 6: DNAT — A Gate Opened

**Kasper** whispered, “Now craft the DNAT — a secret passage from the public IP to the inner world.”

But as **Eks2** wrote `Source: Any`, **Inki** froze.

> “Too open. You didn’t limit source IPs.”

At that very moment, logs blinked. ShadowNet was watching.

It did not attack. It simply... waited.

---

### 🔧 Scene 7: DNS Configuration

“DNS is the memory of names,” **I.K.** shared gently. “Without it, we forget how to reach each other.”

**Eks2** configured the custom DNS IPs. A sense of completeness stirred in him.

---

### 🧪 Scene 8: The Test

From *NordicJump*, he reached *NordicWork*. He opened the browser.

Google — success. Microsoft — blocked.

His firewall was **speaking truth**.

---

### 🌫️ A Presence in the Logs

Later, as the team debriefed, **Eks2** stayed behind.  
He opened the logs.  
Saw faint, unexplained pings.  
Someone had tried port 3389.

Not a full scan. Not an attack.  
Just… curiosity. Silent. Observing.

**ShadowNet** had walked the edge of his cloud.  
Not to break in. But to **remind**.

---

## 🌍 Final Realization – Eks2 Reflects

> “Today, I did more than build a firewall.  
> I learned how **every permission is a reflection of my integrity**.  
> Every port I open — even for testing — is a vow.  
> In Azure, structure isn’t just for access. It’s for accountability.”

He wrote in his notebook:

- “Firewall = *Brandvæg*”  
- “Trust = *Tillid*”  
- “I am not just a learner. I am a quiet protector now.”

---

### 🕶️ ShadowNet’s Whisper

> “I do not strike.  
> I wait.  
> In your convenience.  
> In your forgetfulness.  
> In your comfort.”

---

✍️ Created & Curated by  
**Muhammad Naveed Ishaque**  
_Content Creator | AI Writer | Narrative Simplifier_  
_With the inner voice of Eks2 — the whisper behind the work._

**Siraat AI Academy**  
_“The Straight Path — Empowering minds with clarity, illuminating paths with purpose.”_
