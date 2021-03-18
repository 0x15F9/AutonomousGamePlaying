
To allow human to play game, run the following:

```python
import gym
from gym.utils import play
env = gym.make('Breakout-v0')
gym.utils.play.play(env, zoom=3)
```

---

00
===

Code from DRLHO/Chapter 6

01
===

From 00

- [x] Apply custom Pong preprocessing
- [x] Train till score = 12

02
===

From 01

- [x] Implement model saving and load
- [x] Train till score = 8 and save model
- [x] Load model and train till score = 12

03
===

From 02

- [x] Apply Custom Breakout processing to Rotate (Breakout must be rotated by 90cw)

WRAPPER 1

```
    env = gym.make(env_name)
    env = EpisodicLifeEnv(env)
    env = ClipRewardEnv(env)
    env = NoopResetEnv(env)
    env = MaxAndSkipEnv(env)
    env = FireResetEnv(env)
    env = ProcessFrame84BreakoutRotate(env)
    env = ImageToPyTorch(env)
    env = BufferWrapper(env, 4)
    env = ScaledFloatFrame(env)
```

The reward stagnates around 5. This may be related to the fact that in breakout each game offers 5 lives

WRAPPER 2

```
    env = gym.make(env_name)
    env = NoopResetEnv(env)
    env = MaxAndSkipEnv(env)
    env = FireResetEnv(env)
    env = ProcessFrame84BreakoutRotate(env)
    env = ImageToPyTorch(env)
    env = BufferWrapper(env, 4)
    env = ScaledFloatFrame(env)
```

* RewardClipping is not required since no action yield rewards more than one unit
* The agent is not making proper use of lives (epsidodic life is needed). The failure with wrapper one may indicate that the ordering of wrapper is important

- [x] Train till score = 12
- [x] Train till score = 8 and save model
- [x] Load model and train till score = 12

Loading Breakout models and retraining does not work quite well

- [x] Play using model and watch video to understand problem + also watch obs

in the failed training, there is not proper use of firetorestart. The agent keeps moving left and right, without pressing fire to start the game with next life.
this can be explained as follows:
The training is being resumed with weights adjusted for the last life. However, after the last life there is no need to press fire

WRAPPER 3

```
    env = EpisodicLifeEnv(env)
    env = NoopResetEnv(env)
    env = FireResetEnv(env)
    env = MaxAndSkipEnv(env)
    env = ProcessFrame84BreakoutRotate(env)
    env = ImageToPyTorch(env)
    env = BufferWrapper(env, 4)
    env = ScaledFloatFrame(env)
```

The above wrapper also fails.

WRAPPER 4

```
    env = gym.make(env_name)
    env = EpisodicLifeEnv(env)
    env = MaxAndSkipEnv(env)
    env = FireResetEnv(env)
    env = ProcessFrame84Breakout(env)
    env = ImageToPyTorch(env)
    env = BufferWrapper(env, 4)
    env = ScaledFloatFrame(env)
    return env
```

This wrapper was used in one of my previous attempts. It yielded positive results. Its effectiveness in TL is yet to be determined.

04
===

- [ ] Read report to understand which layers should be retrained
- [ ] Read past implementations to understand how retraining is done
 
04.1
---

From 03 -> 02

- [x] Load Breakout model and train Pong till score = 12 (using only previous weights)

04.2
---

- [ ] Load Pong 8 and Play BreakoutRot till 12

Note: Pong model must contain only for actions for models to be compatible

05
===

- [x] Implement PongRot
- [x] Train PongRot AS 4 till 12

05.1
---

- [ ] PongRotAS4S12 -> Breakout12

```
Note: Naming convention: <ENV_NAME><PreProc><ActionSpace><Score>
```

05.2
---

- [ ] Train Breakout 8
- [ ] Breakout8 -> PongRotAS4

Everything involving playing Breakout fails. Need to investigate the root cause

06
===

Begin Fix Breakout

- [ ] Train Breakout till 8 using WRAPPER 4
- [ ] Visualise
