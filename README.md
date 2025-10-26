# Monopoly-SQL: Relational Database Game Simulation
### 🎲 This project re-creates the Monopoly game purely in SQL — **all you need is to `INSERT` a dice number**, and the players move, pay, and earn automatically.  
### You can even use `RANDINT(1,6)` instead of a fixed number to let the dice roll itself! 🚀
### _Key Stacks: SQL, Database Design_
<br>

## Example Queries

1. **Trigger Dice Roll**:
   ```sql
   INSERT INTO Gamemanager (dice) VALUES (6);
   ```
   
2. **View Game Status**:
   ```sql
   SELECT * FROM gameView;
   ```


<br>

## Examples of gameplay 
### Fixed dice rolls for the example — try RANDINT(1,6) for real gameplay 🎲
<img width="947" height="712" alt="image" src="https://github.com/user-attachments/assets/909a8a6c-6892-40c3-a70f-a3466567b0cb" />

<img width="956" height="817" alt="image" src="https://github.com/user-attachments/assets/721010c0-11ec-4568-9b3e-8a64dca6caf1" />

##

For full gameplay details, refer to the codebase and schema documentation.

_(Monopolee - DATA70141 Coursework (University of Manchester)_

<br>

## Project Overview

This project models a Monopoly game using SQL, providing a complete relational database schema and gameplay logic. The database ensures game integrity with constraints, triggers, and stored procedures while allowing dynamic gameplay through player actions, property management, and game status tracking.

<br>

<img width="1335" height="1837" alt="Flow chart ver 2" src="https://github.com/user-attachments/assets/75534665-c976-4d28-aa89-b6a0b74065e2" />


<br>

### Key Features:
- Comprehensive Entity-Relationship (ER) and relational schema design.
- Trigger-based enforcement of game rules.
- Stored procedures for gameplay mechanics, including player movement, property purchases, and landing effects.
- Audit trail of game actions through the `Gamemanager` table.
- Custom view (`gameView`) to track and visualize game status.

<br>

## Table of Contents
1. [Schema Design](#schema-design)
2. [Gameplay Mechanics](#gameplay-mechanics)
3. [Database Integrity](#database-integrity)
4. [Game Rules Implementation](#game-rules-implementation)
5. [How to Use](#how-to-use)

<br>

## Schema Design

### A. Entity-Relationship Diagram
The ER diagram defines the relationships among key entities like `Player`, `Property`, `Location`, `Bonus`, and `Turns`.

<img width="1402" height="1202" alt="Monopolee (1)" src="https://github.com/user-attachments/assets/49e5eaf9-ecc7-4307-b78b-86784e9c4f11" />

### B. Relational Schema

<img width="1440" height="1668" alt="Monopolee_schema" src="https://github.com/user-attachments/assets/6b56a1e5-04a6-42ac-9e99-5e931b037dac" />


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



<br>

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



<br>

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


<br>

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


<br>

## How to Use

### Setup
1. Import the SQL script into a MySQL database.
2. Execute the schema and initial data insertion queries.

### Starting the Game
1. Use `INSERT INTO Gamemanager (dice)` to simulate dice rolls.
2. Query `gameView` to monitor game progress.


