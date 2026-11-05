ARCADE CAROUSEL — Windows game launcher
========================================

What it does
- Full-screen horizontal game carousel.
- Scans `Games` for time-based games and `Games\Arcade` for internal coin system games.
- Free carousel browsing: players can freely browse the entire library without inserting coins.
- Shows matching cover art automatically when the filename matches.
- Refreshes the library automatically while running.
- Gamepad navigation and launch; keyboard fallback (only keyboard Esc closes the carousel).
- Can be started with Windows using the included batch file.

QUICK START
1. Double-click `install_requirements.bat`.
   - Automatically installs Python 3.12 (if not already installed).
   - Automatically configures Windows System & User PATH.
   - Installs and upgrades pip and pygame.
   - Verifies Tkinter, Pygame, and administrator APIs.
2. Put game shortcuts (`.lnk`) in:
   - `Games\` for Time-Based games (e.g. Tekken 8, GTA V): requires coin credits to launch, shows floating timer overlay, and exits when time expires.
   - `Games\Arcade\` for Arcade / Internal Coin System games (e.g. MAME, RetroArch, arcade ports): starts freely without upfront coins, no timer overlay, no auto-termination.
3. Optional: place cover art in the same folder with the same base name.
   Example:
       Games\Tekken 7.lnk
       Games\Tekken 7.png
       Games\Arcade\Street Fighter III.lnk
       Games\Arcade\Street Fighter III.png
   Supported artwork: PNG, JPG, JPEG, WEBP.
4. Double-click `run_arcade.bat`.
5. To change insert-coin input, time added, or in-game coin key, double-click `run_coin_mapper.bat`.
   Click the input field and press a keyboard key or controller button, D-pad direction,
   stick, or trigger. You can also customize the key sent to arcade games (default '5').

CONTROLS
- Carousel Browsing: Free to browse all games (D-pad Left/Right, Analog Stick, or Left/Right arrows) without inserting coins.
- Insert Coin:
  - In Carousel / Time-Based Games: The configured insert-coin input adds the minutes set in Coin Mapper.
  - In Arcade Games: Pressing the same mapped coin input sends the configured in-game coin key (default '5' for MAME/arcade) directly to the running game window.
- Universal Gamepad Support: Full native XInput (Xbox 360, Xbox One, Xbox Series X/S, 8BitDo, Logitech X-mode), SDL2 GameController, and DirectInput / HID (DualShock 4, DualSense, Switch Pro, USB arcade fightsticks/encoders like Zero Delay and Brook).
- Hot-plugging: Gamepads can be plugged or unplugged at any time while the carousel is running.
- D-pad Left / Right or Left/Right Analog Stick: previous / next game.
- Left Bumper (LB) / Right Bumper (RB): quick jump 5 games backward / forward.
- Gamepad A / Cross or Start button: launch selected game (free for Arcade games; requires coin credit for Time-based games).
- Back / Select button: refresh library.
- Switch Games / Exit to Carousel: Hold Start (or Back / 1P Start) on any controller for 5 seconds to close the current game and return to the carousel.
- Keyboard Backup: Hold Esc or F12 for 5 seconds to close the running game and return to the carousel.
- Keyboard Carousel Controls: Left / Right arrows or A / D, Enter / Space to launch, F5 refresh, Esc to exit carousel launcher.

AUTO-START WITH WINDOWS
1. Double-click `install_autostart.bat` to add a hidden startup entry.
   Alternatively, copy `run_arcade.vbs` into the Startup folder opened with `shell:startup`.
2. Keep the app folder in its current location; the launcher uses its own folder.

NOTES
- This is a Python desktop app. Running `install_requirements.bat` installs all necessary components.
- Direct Native XInput integration via `xinput1_4.dll` / `xinput1_3.dll` guarantees that Xbox/XInput controllers work unconditionally, including detecting coin insertion in the background while heavy games (Tekken 8, GTA V) are running.
- Analog Triggers (LT / RT) on 6-axis controllers are cleanly separated from sticks, preventing trigger pulls from scrolling the carousel.
- The launcher uses Windows' own shortcut handling (`os.startfile`) to open `.lnk` files.
- For Time-Based games: The remaining credit timer stays visible in a floating click-through overlay. When the timer ends, a full-screen click-through 2-minute warning overlay appears. If a coin is inserted within those 2 minutes, normal play resumes; if no coin is added, the game is terminated and the system returns to the Arcade UI.
- For Arcade games: Starts freely; timer overlay is suppressed; no timeout termination occurs; coins inserted during play are forwarded directly to the game via hardware scan code simulation.
- Switching between games: While any game is running, holding Start or Back on any controller (or holding Esc / F12 on a keyboard) continuously for 5 seconds triggers an immediate force-close of the active game and brings the carousel back into fullscreen. An on-screen countdown ('EXITING IN 4... 3... 2... 1...') appears during the hold; releasing the button early cancels the exit.
- Coin Mapper settings are saved in `coin_mapper_config.json` and load automatically in the launcher.
- To exit the full-screen launcher, press Esc on the keyboard (joysticks cannot close the carousel).
- If a shortcut's target requires administrator privileges or a special launcher, Windows may show its usual prompt.
