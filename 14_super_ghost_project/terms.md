**Player** - The application that helps choose and submit one team’s moves. It combines your interface, dictionary logic, and the supplied game components. A player may request a move only through the agreed turn flow; it does not control the opponent or arbiter.

**Arbiter** - The supplied program that announces turns, checks moves, and decides when a game ends. SGhostApp.jar performs this role for Super Ghost. A player’s successful local test does not prove that the arbiter will accept its data or moves.

**Word fragment** - The ordered text made from the letters already played. For example, LAN preserves the order L, A, N. A fragment is not a bag of letters that may be rearranged.

**Dictionary** - The collection of words used to evaluate possible fragments and completed words. PLANET supports the continuous fragment LAN. Use the project’s required data; a tiny practice dictionary does not establish behavior for the full game.

**Shared binary file** - The file through which the supplied programs exchange serialized game records. It contains the project’s agreed object representation rather than the original Ghost text-message format. A file that your player can read back by itself still needs a compatibility check with the arbiter.

**Substring viability** - Whether the complete fragment appears as a continuous sequence somewhere in a dictionary word. LAN appears inside PLANET even though it is not its prefix. Viability does not prove a move is strategically best or that it avoids completing a losing word.

**Move location** - The front-or-back choice sent with the proposed letter. Adding P to the front of LAN makes PLAN; adding E to the back makes LANE. The documented TurnData creation operation uses true for front and false for back, so reversing that flag changes the move.

**Shared class identity** - The agreement between programs about supplied serialized class names, packages, and compatible definitions. The project requires its listed serializable classes under sharedCode. A replacement class with similar fields is not automatically compatible with the arbiter’s class.

**Arbiter-owned state** - Current-turn and game-over values controlled by the arbiter. The player reads GameState and submits a separate action through the supplied path. Submitting an action is not permission to rewrite the arbiter’s state or invent an accepted result.

**Callback contract** - The agreement about when a supplied caller invokes your method, what data it supplies or expects, and which thread runs that method. The source describes onTurn as background selection and updateGUI as a short interface-thread update after successful selection. Read the actual declarations and handoff; being called later does not by itself prove safe shared-state access.
