# 14. Screenshots and evidence

No screenshots are in this repository yet. Nothing is mocked up or presented as evidence. This is the capture plan.

## Shot list

| # | What to capture | Why it matters | Suggested file name |
|---|---|---|---|
| 1 | Desktop home screen | Shows the visual identity | `desktop-home.png` |
| 2 | Dock and launcher open | Shows navigation | `desktop-launcher.png` |
| 3 | Settings window | Shows configuration | `desktop-settings.png` |
| 4 | AI assistant answering a request | Shows the AI surface | `ai-assistant.png` |
| 5 | AI action allowed and recorded | Shows permission and audit | `ai-allowed-audited.png` |
| 6 | AI action denied | Shows the policy refusing | `ai-denied.png` |
| 7 | K1 boot serial output | Shows the banner and boot | `k1-boot-serial.png` |
| 8 | Divide-by-zero test output | Shows exception reporting | `k1-exception-serial.png` |
| 9 | Double-fault test output | Shows the IST path working | `k1-double-fault-serial.png` |
| 10 | Physical allocator test output | Shows allocation checks | `k1-pmm-serial.png` |
| 11 | Page-table inspection output | Shows the paging observations | `k1-vm-inspect-serial.png` |
| 12 | Owned mapper test output | Shows validation and rollback | `k1-owned-mapper-serial.png` |

## Rules

- Capture the real application or a real terminal. No fabricated output.
- Check each image for secrets, tokens, personal data and local machine paths before committing.
- Add alt text and a caption saying whether it shows a working interaction or a prototype.
- For kernel tests, save the plain text log too, since text is easier to verify than an image.
- Label anything that is only a concept visual as a concept visual.
