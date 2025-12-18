# [INTERNAL] Hybrid Gene: System Integration & Conflict Resolution
**Target Audience:** Development & Design Team
**Date:** December 18, 2025
**Reference:** Gatekeep Integration Audit

---

## Overview
During the recent audit of the **Gatekeep** documentation, several critical inconsistencies were identified between the Game Design Document (GDD), technical standards, and active task lists. 

Resolving these conflicts is necessary to unblock production and ensure all team members are working from a single source of truth. Please review the following points and provide a decision for each.

---

## 1. Project Status & Engine Workflow
**The Conflict:** Tasks.md currently lists "Engine Selection" as **BLOCKED**, preventing work on tilesets and plugins. However, Open-Questions.md marks the engine as **DECIDED** (RPG Maker MZ as of Dec 2025).

*   **Question 1.1:** Can we officially move the "Engine Selection" task to **DONE**?
*   **Question 1.2:** If the engine is decided, are there any remaining technical requirements that must be documented before unblocking **Tileset Creation** and **Plugin Development**?

---

## 2. Technical Art Direction (MZ3D Implementation)
**The Conflict:** The plugin standards identify **MZ3D** as a core requirement (for 3D/2.5D rendering), but the art style remains "Open," and sprite standards are currently written for 2D placeholders.

*   **Question 2.1:** Are we committing to **3D Models (.gltf)** or **2D Billboards** (sprites in a 3D environment)?
*   **Question 2.2:** Does the art team have the tools and pipeline to support the chosen format for the 100+ planned monsters, or do we need to revise the **Standards/Sprites.md** doc immediately?

---

## 3. ID Registry & Breeding Mathematics
**The Conflict:** The ID-Register.md allocates IDs **017-050** for Generation 2 (G2) monsters (34 slots). However, the breeding logic (4 species with 10 unique combinations each) requires a minimum of **40 slots** to support a full set of hybrids.

*   **Question 3.1:** Should we expand the G2 ID range to **017-060**? *(Note: This will require a cascading shift of all G3, G4, and Debug IDs).*
*   **Question 3.2:** Alternatively, is there a design reason to limit the number of G2 monsters to 34?

---

## 4. Move Inheritance Logic
**The Conflict:** There is a discrepancy in how offspring learn moves from parents.
*   **GDD Definition:** Child inherits moves that **BOTH** parents know (Intersection logic).
*   **Design Answers:** Child inherits moves that **EITHER** parent knows (Union logic).

*   **Question 4.1:** Which logic should be codified?
    *   **Option A (Intersection):** Higher difficulty; requires strategic "Pure" breeding lines.
    *   **Option B (Union):** Faster progression; allows for "Super-Monsters" with fewer generations.

---

## 5. Combat Systems & Damage Categories
**The Conflict:** The GDD lists Damage Types as "TBD," yet the **Avian** species description already utilizes a **Ranged vs. Melee** damage distinction for its "Flying" trait.

*   **Question 5.1:** Should "Melee" and "Ranged" be officially recognized as the primary damage categories?
*   **Question 5.2:** How do these categories interact with the **Physical/Special** stat split? We need a unified standard in **Standards/Database.md**.

---

## Next Steps
Please submit decisions on these items to the **Gatekeeper**. Once resolved, we will:
1.  Update the ID-Register.md.
2.  Finalize the Standards/ documents.
3.  Update the Tasks.md to **READY** for all currently blocked items.

---
*The Gatekeeper prevents rework.*
