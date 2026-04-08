<h1 align="center">Capture The Flag (AI-Behaviour)</h1>

# Introduction
A Capture the flag game demonstrating AI Behaviour using Behaviour Tress and Finite State Machine in Unreal Engine

## 🎮 How to Download and Play
1. Go to the **Releases** section of this repository.
2. Download the latest `.zip` file.
3. Extract the ZIP to any folder.
4. Double‑click the `.exe` file to start the game.
5. If Windows Security appears:
   - Click **Allow**

#  Game Rule:
1.) The goal is to be able to capture all the other team’s flags and bring them to your team’s side of the field.

2.) Tagging an opponent that is trying to caputre the flag will send them to the prison area

3.) Tagging an imprisoned ally will 'rescue' that ally, and both will return to their base

4.) Defending AI Agents in both teams will:

&nbsp;&nbsp;&nbsp; a.) Try to protect their flags from being captured
  
&nbsp;&nbsp;&nbsp; b.) Prevent opposing players from rescuing their teammate from prison

In 4v4 Gamemode:
- Your ally agents will try and defend while you try to attack by taking flags or rescuing teammates

In 6v6 Gamemode:
- Two attackers are allowed for both teams
- One of your ally agents will atack with you

# AI Behaviour

## The AI Behaviour utilizes Unreal Engine's Behaviour Tree

### 1.) Attack - Capture the Flag

<img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/56a3b52c-c689-48de-9cc6-fee797255ec9" />

- The attacking agent will move to the location of the opposing team’s flag area
- When the agent perceives an opponent’s flag, it moves towards its location to perform collision with it
- Once collided, the agent now carries the flag and must go to the location of its team’s flag area to capture the flag

### 2.) Attack - Rescuing A Teammate

<img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/0e909ece-2c2b-4789-b2a7-29327080fe95" />

- Similar to capturing the flag, the agent will go to location of the opposing team’s prison area.
- The agent will attempt to collide with an imprisoned teammate to free them – causing both agents to return to their base

### 3.) Defending

<img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/80697285-bbdc-4387-8ea4-dbaa81ae5a56" />

- If the agent has detected an enemy, it will try to chase them and tag them by moving to their location
- If the agent has not detected an enemy, then it would patrol to its given patrol area
- The given patrol area is set based on its respective AI Controller which are: General Defender, Prison Defender and Flag Defender

# Assigning AI Roles
## Assigning Roles is handled through a Finite State Machine

### 1.) Choosing new attacking agent

<img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/73e9a88b-936d-46eb-8671-ffe6653ef4fe" />

- When the attacker has been imprisoned, a new attacker will be chosen
- The new attacker is chosen based on its current defending role
- Replacing attacker is based on priority: General Defender first then Prison Defender then Flag Defender

### 2.) Choosing what kind of attack to perform (either Capture Flag or Rescue Teammate)

<img width="640" height="450" alt="image" src="https://github.com/user-attachments/assets/39e95c49-64b2-4283-9442-a818eda12365" />

- Choosing the kind of attack to perform is based on the team’s current score and current number of imprisoned teammates.
- If the current number of imprisoned teammates is greater than their current score then attack by rescuing teammates.
- If the current score is greater than their number of imprisoned teammates then attack by capturing opponent’s flag
- If equal scores then 50/50 chance of rescuing or attacking flag
- The new attacker is given a new AI Controller with the chosen attack
- After successfully performing its current attacking goal, it will re-evaluate its attack goal by re-checking the current conditions


# AI Steering Behaviour

- When attacking, agent will try and avoid player/other defending npcs while still moving towards its goal (flag location/taking flag home)
- This was done by setting a nav mesh modifier around the defending agent/player with a nav area cost of 10



