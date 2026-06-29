# Hermes Genesis Packet

This folder is the portable **brain** for the Hermes Solana Edge OS build. It exists so that
none of the thinking from the planning sessions stays trapped in a chat window — it lives in
files, so it travels to any repo or any agent without loss.

**How to use it:** when you stand up the clean, private build repo, copy this folder's contents
into it (or into `/docs`). Hand any agent `CONTEXT_PACK.md` as its first read and it will know the
project, the decisions, and the next action.

**Read in this order:**

1. **`CONTEXT_PACK.md`** — what we're building, why, what's verified, what's decided, and the next
   action. The single most important file.
2. **`ADR-000-hermes-build-repo.md`** — the decision to build in a dedicated private repo, recorded
   as an Architecture Decision Record (the pattern you reuse for every consequential choice).
3. **`PORT_LIST.md`** — exactly what to carry over from the `symphony` research hub, and what to
   leave behind.

**What an ADR is (plain English):** an *Architecture Decision Record* is a short, dated note that
says "we decided **X**, because **Y**, and here's what it costs us." One file per decision. It's how
a non-developer keeps an auditable trail of *why* the system is the way it is — so future-you (or an
agent) never has to re-litigate a settled choice.

---

Created: 2026-06-29 · Status: living document — update it as decisions change.
