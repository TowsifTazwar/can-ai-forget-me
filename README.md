# Can AI Forget Me?
### What "delete" means in consumer AI assistants and what people would need to trust it

**Md. Towsif Tazwar Hussain** · Department of CSE, United International University, Dhaka
Independent research brief · November 2026

> **Type of work:** desk review of official documentation plus design requirements. No users were studied and no app was tested. Findings describe what providers *say* in their help pages, not measured system behaviour. A user study is proposed as the next step (Section 7).

---

## 1. Why I am asking this

Data protection laws give people a right to have their data erased. For AI this raises a harder question: a model trained on someone's data should then behave as if it never saw them. Making that happen is called **machine unlearning**.

Research on machine unlearning, including my own ongoing work on tabular models, points to a gap between deleting data in principle and deleting it in practice. Exact deletion is possible, for example by retraining on the remaining data [1]. But data about a person can persist in more places than the obvious one. Prior work has also shown that comparing a model's outputs before and after a deletion can reveal who was deleted [2].

So even when the engineering is right, the human side stays open: **when a person presses "delete", what do they believe happens and how could they ever know it did?** This brief is a first step toward that question.

## 2. Questions

- **Q1.** What do popular AI assistants tell people that "delete" covers?
- **Q2.** Where does that wording leave gaps compared with what can technically remain after deletion?
- **Q3.** What should a "forget me" experience show people so they can understand and trust it?

## 3. Method

I read the official help and privacy pages of three assistants widely used in Bangladesh: **ChatGPT** (OpenAI), **Gemini** (Google) and **Meta AI** (available inside Facebook, Messenger, Instagram and WhatsApp). Pages were accessed on 22 November 2026.

I coded each provider against seven **layers of deletion**, covering the places a person's data can persist in an AI service, from visible history to models already trained:

| Layer | Question asked of each provider |
|---|---|
| L1 Visible history | Does deleting remove the chat from my view? |
| L2 Stored copies | How long until it is removed from the provider's systems and with what exceptions? |
| L3 Reviewed copies | Are copies seen by human reviewers kept separately? |
| L4 Memory | Is what the assistant "remembers" about me deleted by the same action? |
| L5 Future training | Can I stop my chats being used to train future models? |
| L6 Past training | What happens to models *already* trained on my data? |
| L7 Proof | Do I get any confirmation or record that deletion happened? |

## 4. What the providers say

| Layer | ChatGPT | Gemini | Meta AI |
|---|---|---|---|
| **L1 Visible history** | Removed from account view immediately | Chats can be deleted manually at any time | "Delete all chats and media" removes chats from History and Media in the Meta AI app |
| **L2 Stored copies** | Scheduled for permanent deletion within 30 days, unless already de-identified or kept for security or legal reasons | With History off, chats are still kept with the account for about two months. History auto-deletes after 18 months by default | Not stated on the deletion help page |
| **L3 Reviewed copies** | Not stated on the pages reviewed | Human-reviewed chats are separated from the account and kept for up to 3 years, even after the user deletes them | Not stated |
| **L4 Memory** | Memory is a separate control from training; deleting a chat is a separate action | Memory and past-chat personalisation are separate settings | Not stated on the deletion page |
| **L5 Future training** | "Improve the model for everyone" toggle. Turning it off does not delete saved chats. Thumbs-up/down feedback can lead to the whole conversation being used for training even with the toggle off | Separate setting for chat content training. Submitting feedback is an exception | "Meta uses your interactions with AIs to improve AI at Meta." No opt-out described on the deletion page |
| **L6 Past training** | Not stated | Not stated | Not stated |
| **L7 Proof** | None described; deleted chats cannot be restored | None described | None described |

## 5. Observations

**O1. "Delete" mostly means "remove from your view".** All three providers describe deletion first as disappearance from history. Removal from their systems follows on the provider's own timeline (30 days for ChatGPT) and with exceptions (up to 3 years for human-reviewed Gemini chats).

**O2. People must assemble deletion themselves.** Chat deletion, memory, history settings and training settings are separate controls. Someone who wants to be "forgotten" has to know which controls exist and use all of them.

**O3. Small actions can carry large, easy-to-miss consequences.** Both OpenAI and Google state that giving feedback on a response can bring a conversation into training even when the person has opted out. A thumbs-up looks trivial; its effect on privacy is not visible at the moment it is pressed.

**O4. Nobody talks about models already trained.** None of the pages I reviewed says what happens to a model that has *already* learned from someone's data (L6). This is exactly the layer machine unlearning research is about and it is invisible to users.

**O5. There is no proof.** No provider describes a receipt, log or any way for a person to check that deletion happened (L7). Unlearning research shows that deletion *can* be verified technically, for example by comparing a model with one rebuilt without the person's data. Today only someone with system access could do that.

## 6. Design requirements for a trustworthy "forget me" flow

These connect technical realities of deletion (left) to what a person would need to see (right).

| Technical reality | Design requirement |
|---|---|
| Data about a person can persist in several places beyond the visible chat | **R1. Show the layers.** Say plainly which layers an action deletes and which it does not, in the person's own language (for Bangladesh, Bangla first). |
| Full removal takes time and has legal exceptions | **R2. Give a clear timeline.** Say when deletion will be complete and name the exceptions in plain words. |
| Partial deletion can fail without anyone noticing | **R3. One "forget me" entry point** that covers chats, memory and training use together, instead of four separate settings. |
| Deletion can be verified when every deletion is logged | **R4. A deletion receipt** stating what was deleted and when, which the person can keep and an auditor could verify. |
| Deletion itself can reveal who asked [2]; past training may not be undone | **R5. Be honest about limits.** Say what deletion cannot guarantee, including models already trained, rather than implying everything is gone. |
| Exceptions are triggered by ordinary actions | **R6. Show side effects at the moment they happen**, for example a short note on feedback buttons when training is turned off. |

These are hypotheses to test with people, not validated guidelines.

## 7. Proposed next step: a mental-model interview study

- **Who:** 12–15 smartphone users in Dhaka, mixing university students and people outside tech, including people who use Meta AI inside Messenger or WhatsApp.
- **How:**
  1. Semi-structured interviews about what they think happens when they delete a chat or ask an AI to forget something.
  2. A short drawing task: "Show me where your message goes after you press delete."
  3. A card-sorting task using the seven layers, asking which layers they expect a "delete" button to cover.
  4. Feedback on paper sketches of a deletion receipt (R4) and a layered explanation (R1).
- **Analysis:** thematic analysis of interview transcripts, comparing expectations against the layers in Section 4.
- **Ethics:** informed consent, no collection of chat content, anonymised transcripts and institutional ethics approval before recruiting.

## 8. Limitations

- Help pages describe policy, not verified system behaviour.
- Pages change often; this is a snapshot from 22 November 2026.
- Only three assistants were reviewed and only in English.
- "Not stated" means not stated on the pages I reviewed. A provider may explain it elsewhere.
- The coding was done by one person, the author.

## References

1. Bourtoule, L., Chandrasekaran, V., Choquette-Choo, C. A., Jia, H., Travers, A., Zhang, B., Lie, D. & Papernot, N. (2021). Machine Unlearning. *IEEE Symposium on Security and Privacy*.
2. Chen, M., Zhang, Z., Wang, T., Backes, M., Humbert, M. & Zhang, Y. (2021). When Machine Unlearning Jeopardizes Privacy. *ACM Conference on Computer and Communications Security (CCS)*.

## Sources (accessed 22 November 2026)

- OpenAI Help Center, [Deleting and archiving chats in ChatGPT](https://help.openai.com/en/articles/8809935-deleting-and-archiving-chats-in-chatgpt)
- OpenAI Help Center, [Data controls FAQ](https://help.openai.com/en/articles/7730893-data-controls-faq)
- Google, [Gemini Apps Privacy Hub](https://support.google.com/gemini/answer/13594961?hl=en) (last updated 19 November 2026)
- Meta Help Center, [Remove posts, chats and media from Meta AI and Vibes](https://www.meta.com/help/artificial-intelligence/2457110494637611/)
- Meta Newsroom, [Privacy Matters: Meta's Generative AI Features](https://about.fb.com/news/2023/09/privacy-matters-metas-generative-ai-features/) (2023, updated 2025)
