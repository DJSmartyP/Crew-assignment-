# Bridge Command Crew Allocator

A static, GitHub Pages-ready web app for assigning 28 players across two 14-person bridge-command crews.

## Fixed ships
- Takanami
- Havock

## Positions on each ship
### Main ship bridge
1. Captain
2. Helm
3. Beams
4. Missiles
5. Nav
6. Radar
7. Dock and drone
8. Comms
9. Engineering
10. Manual engineer

### Ship shuttle
11. Shuttle helm
12. Shuttle generalist
13. Shuttle engineer
14. XO (second in command)

## Player input
Each player can enter:
- Name
- Preferred ship: Takanami, Havock, or no preference
- 1st station choice
- 2nd station choice
- 3rd station choice
- Any number of stations they **really don't want**

The three ranked choices must be different, and a ranked choice cannot also be marked as a disliked station.

## Allocation priority
The optimiser uses a lexicographic priority order:
1. Maximise 1st-choice assignments.
2. Then maximise 2nd-choice assignments without reducing the number of 1st choices.
3. Then maximise 3rd-choice assignments without reducing the higher priorities.
4. Then avoid stations marked **really don't want**.
5. Then satisfy ship preference.
6. Finally use a tiny tie-break value to choose between otherwise equivalent layouts.

This means station preference is deliberately more important than preferred ship.

The loadout recalculates with fewer than 28 players, so the board can be watched filling up as preferences are entered. Empty roles are shown as vacant. When all 28 are present, every position on both ships is filled.

A "really don't want" role is not an absolute prohibition: it is treated as a last-resort assignment. Any such assignment is highlighted clearly on the board.

## Data
Preferences are saved to `localStorage` in the browser. The organiser can also export and import a JSON backup.

## GitHub Pages
1. Create a repository.
2. Upload `index.html` (and this README if wanted).
3. In GitHub open **Settings → Pages**.
4. Choose **Deploy from a branch**, select `main`, `/ (root)`.
5. Save.

## Multi-device limitation
This version is static/serverless. If 28 people each open the GitHub Pages URL on separate phones, those devices will have separate local datasets and will **not** automatically merge into one shared board.

For genuine simultaneous submissions from 28 separate phones, a small shared backend (for example Supabase or Firebase) should be added. The allocation/UI can stay the same.
