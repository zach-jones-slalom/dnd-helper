# Functional Requirements - MTG Swiss Manager

## Overview
A comprehensive web application for managing Magic: The Gathering (MTG) Swiss-style tournaments, providing tournament organizers with tools to handle player registration, automated pairings, match result tracking, and final standings calculation.

## Core Features

### 1. Player Management

#### 1.1 Add Player
- **Description**: Tournament organizers can register new players for the tournament
- **Required Fields**:
  - Name (string, required, max 255 characters)
  - Existing Score (string, optional, format: "wins-losses-draws" e.g., "2-1-0")
- **Behavior**:
  - New players start with zero wins/losses/draws unless existing score provided
  - Players are added to the tournament roster immediately
  - Duplicate names are allowed (handled by unique IDs)

#### 1.2 View Players
- **Description**: Display all registered players with their current tournament statistics
- **Display Information**:
  - Player name
  - Current record (wins-losses-draws)
  - Total tournament points
  - BYE history indicator
- **Ordering**: Players displayed in order of addition

#### 1.3 Remove Player
- **Description**: Remove a player from the tournament roster
- **Behavior**:
  - Player is permanently removed from the tournament
  - All existing pairings are cleared when a player is removed
  - Tournament round resets to 1

### 2. Tournament Pairing System

#### 2.1 Generate Round Pairings
- **Description**: Automatically create fair matchups for the current tournament round
- **Behavior**:
  - Players grouped by current tournament points
  - Pairings avoid repeat matchups from previous rounds
  - Odd number of players results in BYE assignment
  - BYE prioritizes players without previous BYEs
  - Pairings generated instantly upon request

#### 2.2 View Current Round Pairings
- **Description**: Display all matchups for the active tournament round
- **Display Information**:
  - Table number assignment
  - Player names for each matchup
  - BYE assignments clearly indicated
- **Behavior**: Pairings shown in order of table number

#### 2.3 Advance Tournament Round
- **Description**: Progress to the next round after current round completion
- **Behavior**:
  - Requires all matches in current round to be reported
  - Automatically increments round counter
  - Enables generation of next round pairings

### 3. Match Result Management

#### 3.1 Report Match Results
- **Description**: Record the outcome of individual matches
- **Required Fields**:
  - Result selection (win/loss/draw for both players, mutually exclusive)
- **Behavior**:
  - Results update player records immediately
  - Match marked as reported once result submitted
  - Changes reflected in real-time standings

#### 3.2 Track Match Completion
- **Description**: Monitor progress of current round matches
- **Display Information**:
  - Number of completed matches vs total matches
  - Visual indicators for reported vs unreported matches
- **Behavior**: Updates automatically as results are reported

### 4. Tournament Standings

#### 4.1 Calculate Real-time Standings
- **Description**: Compute and display current tournament rankings
- **Tiebreaker System**:
  - Primary: Total tournament points
  - Secondary: Win percentage
  - Tertiary: Strength of Schedule (average opponent points)
  - Additional: Head-to-head results, games played, alphabetical
- **Behavior**: Standings update automatically after each match result

#### 4.2 Display Final Standings
- **Description**: Show comprehensive tournament results upon completion
- **Display Information**:
  - Player ranking with podium indicators
  - Complete record including BYEs
  - Win percentage and Strength of Schedule
- **Behavior**: Automatically shown when tournament reaches final round

### 5. Data Persistence and Management

#### 5.1 Automatic Data Saving
- **Storage Mechanism**: Use the existing backend persistence mechanism (Express.js API)
- **Data Durability**: All tournament changes are persisted to the backend
- **Behavior**:
  - All changes saved immediately via API calls to backend
  - Tournament data persists in backend storage
  - Data automatically loaded from backend on application startup

#### 5.2 Import/Export Tournament Data
- **Description**: Backup and restore tournament data via JSON files
- **Behavior**:
  - Export creates downloadable JSON file with complete tournament state
  - Import validates and loads tournament data from JSON file
  - Success/failure feedback provided to user

#### 5.3 Tournament Reset
- **Description**: Clear all tournament data and start fresh
- **Behavior**:
  - Confirmation required before reset
  - Completely clears player roster and pairings
  - Resets tournament to initial state

### 6. Tournament Configuration

#### 6.1 Set Tournament Rounds
- **Description**: Configure the number of rounds for the tournament
- **Options**: 3-8 rounds (configurable range)
- **Behavior**:
  - Setting locked once tournament begins (pairings generated)
  - Default of 4 rounds if not specified

## Out of Scope

- User authentication and multi-user support
- Player deck registration or deck validation
- Advanced tournament formats (single elimination, round-robin)
- Player ratings or ranking systems beyond Swiss points
- Tournament scheduling or time management
- Communication features (announcements, chat)
- Statistical analysis beyond basic standings
- Mobile application development
- Integration with external MTG databases or APIs
- Tournament fee management or payment processing
- Player check-in or attendance tracking

## Technical Constraints

- Frontend: React 19 with TypeScript, built with Vite
- Backend: Express.js API for data persistence
- Single-user application (no user accounts or data isolation)
- Desktop-focused interface (no mobile optimization required)
- Data persisted via backend API

## Success Criteria

- [ ] User can add players with optional existing scores
- [ ] User can view all players with current records and points
- [ ] User can remove players (with tournament reset)
- [ ] User can generate fair Swiss pairings for each round
- [ ] User can view current round pairings with table assignments
- [ ] User can report match results (win/loss/draw)
- [ ] User can track match completion progress
- [ ] User can advance to next round after completion
- [ ] User can view real-time standings with proper tiebreakers
- [ ] User can view final standings with podium recognition
- [ ] Tournament data automatically saves to backend via API
- [ ] User can import/export tournament data as JSON
- [ ] User can reset tournament with confirmation
- [ ] User can configure number of tournament rounds
- [ ] Simple, intuitive interface for tournament management