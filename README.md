# PlayRoom Premium — Multiplayer Game Platform (v5)

Two-player real-time games (**40 games**). Midnight-violet theme with **Gold = Player 1** and **Pink = Player 2**.
Fully responsive (mobile, tablet, desktop).

## What's new in v5
- **🎙️ Live voice chat** between the two players (like PUBG voice). Both press **Join voice** in the room, allow the microphone, and you can talk. Mute button + a green ring around the avatar of whoever is speaking. It is WebRTC, so the audio goes directly between the two phones/PCs, not through your server.
  - Needs **HTTPS** (or `localhost`) — browsers block the microphone on plain `http://`. Render / Railway / Vercel-style hosting gives you HTTPS automatically.
  - Works on most networks with the built-in free STUN servers. On very strict mobile/office networks add a **TURN** server by setting the env vars `TURN_URLS`, `TURN_USERNAME`, `TURN_CREDENTIAL` (e.g. a free account from metered.ca or your own coturn).
  - Use headphones to avoid echo.
- **🪜🐍 Snake & Ladder** (new game #40): 10×10 board, dice, ladders up / snakes down, 6 = roll again (three 6s = turn lost), reach 100 first.
- **🎚️ Levels — Easy / Medium / Hard**: pick in the room (either player; applies from the next round). Games that change with the level are marked 🎚️ LEVELS:

| Game | Easy | Medium | Hard |
|---|---|---|---|
| Snake & Ladder | 7 ladders, 4 short snakes, any roll that reaches 100 wins | 7 ladders, 8 snakes, exact roll for 100 | 5 ladders, 10 long snakes, exact roll for 100 |
| Snake Battle | slow, first to 7 | normal, first to 10 | fast, first to 12 |
| Math Battle | small numbers, first to 3 | normal, first to 3 | big numbers, first to 5 |
| Number Guess | 1–50 | 1–100 | 1–500 |
| Memory Match | 6 pairs | 8 pairs | 10 pairs |
| Pig Dice | first to 30 | first to 50 | first to 100 |
| Maze Race | 9×9 | 11×11 | 15×15 |
| Whack-a-Mole | moles stay longer | normal | fast moles |

- **🗣️ Winner voice fixed**: now says a clear **"Raghav wins!"** (name + wins). It waits for the win jingle to end, picks the best English voice on the device (Indian English first, natural/neural voices preferred) and speaks slower. Turn it on/off with the 🗣️ button.

## What's new in v4.1
- **Points are now separate for every game.** The player cards show the points of the game you are in (e.g. "pts · Ludo"); a 📊 Scoreboard table lists every game with both players' points, wins, rounds and a grand total.
- **Speaker buttons** in the header: 🔊 sound effects on/off and 🗣️ voice announcements on/off (remembered on your device). Sounds: tap, your-turn ping, win / lose / draw jingles, emoji pop.

## What's new in v4
- **23 new games** (all 36 titles from your list are now in, plus 3 bonus games: Number Duel, Five in a Row, Pig Dice).
- **Rules screen in English + Hinglish before every game.** Both players press "I'm ready" and only then does the round start. "Play again" skips the rules.
- **Emoji reactions**: tap the 😀 button (bottom-right), pick from 30 emojis or type/paste ANY emoji. It floats up on both screens with the sender's name.
- **Category tabs** in the game picker (Classic & Board, Arcade & Action, Racing & Sports, Puzzle & Brain, Funny & Unique).
- Renamed to match your list: Math Race -> Math Battle, Higher or Lower -> Number Guess, Reaction Race -> Reaction Duel, Reversi -> Reversi (Othello).

| New game | How it runs |
|---|---|
| Ludo, Dominoes, Mancala, Tank Battle, Football Penalty, Basketball Duel, Word Scramble, Quiz Battle, Code Breaker, Sequence Memory, Color Pattern Duel, Maze Race, Whack-a-Mole, Draw & Guess | Server-authoritative (secrets such as hands, codes, answers and words never reach the other player) |
| Snake Battle, Pong Duel, Air Hockey | Live server physics loop (about 30 updates per second) |
| Brick Breaker Duel, Space Shooter, Platform Race, Car Racing, Bike Racing, Mini Golf | Both players play the same seeded level on their own device at the same time; final scores are sent to the server which picks the winner. Live scores are shown during play |

Notes: Bike Racing uses the same lane-dodge engine as Car Racing with 4 lanes and higher speed. Draw & Guess sends each stroke when the drawer lifts the finger.

New files: `extra.js` (server logic of the 23 games), `public/rules.js` (rules text), `public/games2.js` (client screens), `public/arcade.js` (local arcade engines).

## What was new in v3
- **New colour system**: deep midnight violet background, gold and pink player colours, clear contrast everywhere.
- **Points under each player's name**: a win gives the winner **+10 points**, a draw gives **+3 each**.
  Points animate (count-up and a floating "+10"), the leader gets a crown, wins are counted with a trophy.
- **Winner celebration**: a popup with the winner's name, "+10 points for <name>", the scoreboard and confetti.
  Voice announcement on both devices: "Congratulations <name>! You won!"
- **Names everywhere**: messages say "Aarav's turn" instead of "X's turn". The turn bar turns green on your turn.
- **Starter alternates** every round.
- **No cheating**: the server no longer sends secrets (hangman word, enemy ships, hidden picks, secret number) to the other player.

## Game fixes and upgrades
| Game | What changed |
|---|---|
| Tic Tac Toe | Winning line highlighted, bigger responsive board |
| Rock Paper Scissors | Big cards, picks hidden until both choose, reveal screen |
| Connect Four | Drop animation, winning four glows, larger discs |
| Dots & Boxes | Fixed broken board (game could never finish). Now 5x5 boxes (25, so no draws), lines coloured by player |
| Hangman | 27 random words with category, drawn gallows, players alternate turns |
| Battleship | 8x8 grid, fleet of 3 ships (4/3/2), rotate / random / reset / ready, separate enemy and own grids, hit and miss look different, extra shot on hit |
| Checkers | Captures, compulsory jumps, multi-jumps, kings and win detection, legal squares highlighted |
| Chess | Legal-move dots, last move, check highlight, board flips for Black |
| Number Duel | Reveal screen with both numbers |
| Higher or Lower | Live range bar, shared guess history |

## New games in this update (16 games total)
| Game | How it works |
|---|---|
| Memory Match | 4x4 cards, 8 pairs. Find a pair to score and go again. Cards stay hidden on the server until flipped |
| Reversi | 8x8 board, glowing legal squares, auto-pass when a player has no move, most discs wins |
| Five in a Row (Gomoku) | 11x11 board, first to make 5 in a line wins, winning line glows |
| Reaction Race | Screen is red, turns green at a random moment. First tap wins, tapping early loses |
| Math Race | Same question for both players. First to 3 correct answers wins; a wrong answer locks you out of that question |
| Pig Dice | Roll to build a turn total, roll a 1 and lose it, hold to bank. First to 50 wins |

## Run locally
Node.js 18+:
```bash
npm install
npm start
```
Open http://localhost:3000

## Deploy (Render)
Push the whole project to GitHub, create a Web Service, Build `npm install`, Start `npm start`.
Do not host only the `public` folder on static hosting; Socket.IO needs the Node server.

## Notes
- Rooms and scores live in memory and reset if the server restarts.
- The voice announcement uses each device's own SpeechSynthesis; browsers may need a tap first and device volume on.
