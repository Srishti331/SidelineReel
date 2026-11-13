# SidelineReel · Confident Roster Tagging (prototype)

**Live demo:** https://srishti331.github.io/SidelineReel/

A working prototype built for the [Ajaia](https://ajaia.ai) Product Manager assessment. SidelineReel is Ajaia's app for youth sports clubs: coaches upload game footage, and the app cuts each kid's highlights into a personal reel and sends a weekly team recap to every family.

## The problem
Roster tagging, which matches a jersey number in the footage to a name on the roster, sometimes sends **the wrong kid's highlight** to a family. This week's support tickets came from three different clubs, and all showed the same pattern: look-alike numbers (4 vs 14, 1 vs 11, swapped digits like 12/21).

It's also hidden in the headline metric. The **92% Reel Share Rate** only counts reels that were opened. Around 30% of reels are never opened, and wrong-kid thumbnails are one named cause. Measured over every reel generated, the share rate is about **64%**.

## What the prototype does
The fix is a confidence gate with a human in the loop:

| Step | Who | What happens |
|---|---|---|
| 1. Hold | System | A clip is held from personal reels if confidence < 85%, **or** its number has a look-alike on the roster and confidence < 97%. |
| 2. Confirm | Coach | Sees *why* each clip was held ("#11 looks like #1 on this roster") and assigns it with one tap. |
| 3. Send | Coach | Unreviewed clips are left out of personal reels, never guessed. They appear untagged in the team recap, and the coach is warned before sending. |
| 4. Catch | Parent | One tap on **Not my kid** removes a clip that slipped through and sends it back to the coach to re-tag. |

Thumbnails are only ever chosen from confirmed or high-confidence clips.

## Try it (about 2 minutes)
The in-page **Try it** checklist guides you through the steps:
1. **Coach: Review held clips.** Assign the #11 Goal (19:33) to **#1 Ava**.
2. **Parent: My kid's reel.** As **#14 Sofia**'s parent, tap **Not my kid** on the 41:17 Big play.
3. **Coach: Review.** Re-tag that flagged clip to **#4 Mia**.
4. **Coach: Reels & recap.** Click **Approve & schedule**. You'll see the warning about unreviewed clips.

The **How clips get held** tab shows the look-alike pairs computed from the roster, with live threshold sliders.

## What's real and what's simulated
- **Real:** look-alike detection (number contained in another, swapped digits, visually similar digits), the hold rules, the review, flag and send state, and the thumbnail rule.
- **Simulated:** model confidence scores and the video frames. Real computer vision is out of scope, and all names are invented sample data.
- **Deliberately out of scope:** face recognition or any biometric ID of children.

## Tech
A single self-contained `index.html` (HTML, CSS and vanilla JS) with no build step and no dependencies. Open it locally or serve it with GitHub Pages.

---
Built by Srishti, with Claude used as a build partner. The product decisions are mine.
