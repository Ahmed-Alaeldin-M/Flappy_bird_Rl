# Flappy Bird Reinforcement Learning

This project implements a **Flappy Bird game** using **Reinforcement Learning (RL)** with the **PPO (Proximal Policy Optimization)** algorithm. The RL agent learns to play the game by interacting with the environment and improving its performance over time.

---

## Project Structure

| File              | Description                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------- |
| `flappy.py`       | Main source code containing the game environment logic (`reset`, `step`, `render`, `quit`). |
| `flappyenv.ipynb` | Custom environment initialization, training, and testing of the RL agent.                   |
| `PPO_500000.zip`  | Pre-trained PPO model weights after 500,000 training steps.                                 |

---

## How It Works

1. **Environment**

   * The environment simulates the Flappy Bird game.
   * Key methods:

     * `reset()`: Resets the game to the starting state.
     * `step(action)`: Applies an action (jump or do nothing) and returns the new state, reward, and termination info.
     * `render()`: Displays the game on the screen.
     * `quit()`: Closes the game window and cleans up resources.

2. **Training**

   * The agent is trained using the PPO algorithm.
   * Observations: Game screen state (or simplified state representation).
   * Actions: Jump or do nothing.
   * Reward: Surviving longer and passing through pipes gives positive rewards.

3. **Testing**

   * After training, load the pre-trained model and watch the agent play:

```python
from stable_baselines3 import PPO
from flappyenv import FlappyEnv

env = FlappyEnv()
model = PPO.load("PPO_500000.zip", env=env)

obs, info = env.reset()
while True:
    action, _ = model.predict(obs, deterministic=True)
    obs, reward, terminated, truncated, info = env.step(action)
    env.render()
    if terminated:
        break
env.close()
```

---

## Screenshots

**Game Environment:**
![Flappy Bird Game](imgs/img_45.png)

**Training Progress:**
![Training Reward Curve](images/reward_curve.png)

**Agent Playing:**
![Agent Playing](images/agent_playing.png)

*(You can generate screenshots during gameplay and training and save them in an `images/` folder.)*

---

## Usage

Install dependencies:

```cmd
pip install pygame stable-baselines3 gymnasium
```


