# Monopoly-SQL: A Relational Database Implementation for Monopoly Game

## Project Overview

This project models a Monopoly game using SQL, providing a complete relational database schema and gameplay logic. The database ensures game integrity with constraints, triggers, and stored procedures while allowing dynamic gameplay through player actions, property management, and game status tracking.

![flow_chart_monopolee](https://github.com/user-attachments/assets/6259bb2d-e0fc-4362-aa18-719eda0901d7)

### Key Features:
- Comprehensive Entity-Relationship (ER) and relational schema design.
- Trigger-based enforcement of game rules.
- Stored procedures for gameplay mechanics, including player movement, property purchases, and landing effects.
- Audit trail of game actions through the `Gamemanager` table.
- Custom view (`gameView`) to track and visualize game status.

---

## Table of Contents
1. [Schema Design](#schema-design)
2. [Gameplay Mechanics](#gameplay-mechanics)
3. [Database Integrity](#database-integrity)
4. [Game Rules Implementation](#game-rules-implementation)
5. [How to Use](#how-to-use)

---

## Schema Design

### Entity-Relationship Diagram
The ER diagram defines the relationships among key entities like `Player`, `Property`, `Location`, `Bonus`, and `Turns`.

![image](https://github.com/user-attachments/assets/14f3cf8a-937b-4d48-b00f-f601d5b84aa2)

---

### Relational Schema

![image](https://github.com/user-attachments/assets/9049bd9a-bcb3-403a-80d4-e896364a6b35)

1. **Location Table**
   - Tracks all game tiles (bonus or property).
   - `type` column distinguishes tile type (0 for bonus, 1 for property).

2. **Player Table**
   - Stores player information, including bank balance and location.
   - `token` column ensures unique player tokens.

3. **Property Table**
   - Manages property ownership, costs, and color categorization.

4. **Bonus Table**
   - Defines bonus tiles and their effects.

5. **Gamemanager Table**
   - Tracks game progress, including dice rolls, player turns, and bank balances.

6. **gameView**
   - A dynamic view that shows game status, including player properties, locations, and bank balances.

---

## Gameplay Mechanics

### Key Procedures and Functions
1. **Player Movement (`move_player`)**
   - Moves a player based on dice rolls and updates their location.
   - Awards bonuses for passing the `GO` tile.

2. **Landing Effects (`player_landing`)**
   - Determines actions based on the tile type (property or bonus).
   - Calls specialized procedures for property or bonus tiles.

3. **Property Management (`landing_on_property`)**
   - Handles rent payments, property purchases, and ownership transfers.

4. **Bonus Effects (`landing_on_bonus`)**
   - Activates effects such as rewards, fines, or sending a player to jail.

5. **Game Status Updates (`select_next_player`)**
   - Advances the turn and checks for round completions.

6. **Monopoly Check (`monopoly_checker`)**
   - Doubles property rent if a player monopolizes a color.

---

## Database Integrity

### Constraints
- `UNIQUE` constraints on property and bonus locations.
- Foreign keys enforce referential integrity between related tables.

### Triggers
- **Player Registration (`add_player`)**:
  - Limits the game to six players.
- **Location Type Checks**:
  - Prevents assigning bonus tiles to property locations and vice versa.

### Stored Procedures
- Manage player actions, enforce game rules, and handle exceptions (e.g., bankruptcy).

---

## Game Rules Implementation

### Highlights
1. **Bankruptcy**:
   - Players unable to pay rent or bonuses lose all properties and are removed from the game.

2. **Jail Rules**:
   - Players must roll a 6 to escape jail.

3. **Color Monopolies**:
   - Rent doubles when a player monopolizes a property color.

4. **Winning Condition**:
   - The last player standing is declared the winner.

### Dynamic Gameplay
- Dice rolls (`dice_trigger`) control player actions.
- Session variables track game state (`@turn`, `@round`, etc.).

---

## How to Use

### Setup
1. Import the SQL script into a MySQL database.
2. Execute the schema and initial data insertion queries.

### Starting the Game
1. Use `INSERT INTO Gamemanager (dice)` to simulate dice rolls.
2. Query `gameView` to monitor game progress.

### Example Queries
1. **Player Movement**:
   ```sql
   CALL move_player(player_ID, dice);
   ```

2. **View Game Status**:
   ```sql
   SELECT * FROM gameView;
   ```

3. **Trigger Dice Roll**:
   ```sql
   INSERT INTO Gamemanager (dice) VALUES (6);
   ```

---

For full gameplay details, refer to the codebase and schema documentation.
