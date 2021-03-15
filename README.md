00
===

Code from DRLHO/Chapter 6

01
===

From 00

[x] Apply custom Pong preprocessing

[x] Train till score = 12

02
===

From 01

[x] Implement model saving and load

[x] Train till score = 8 and save model

[x] Load model and train till score = 12

03
===

From 02

[ ] Apply Custom Breakout processing to Rotate (Breakout must be rotated by 90cw)

WRAPPER 1

> 12257: done 354 games, mean reward 0.340, eps 0.88, speed 11.56 f/s max reward 0.333

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

> 12548: done 474 games, mean reward 0.090, eps 0.87, speed 9.45 f/s max reward 0.3

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

RewardClipping is not required since no action yield rewards more than one unit

[x] Train till score = 12

[x] Train till score = 8 and save model

[x] Load model and train till score = 12

Loading Breakout models and retraining does not work quite well

[ ] Play using model and watch video to understand problem + also watch obs

04
===

[ ] Read report to understand which layers should be retrained

[ ] Read past implementations to understand how retraining is done
 
From 03 -> 02

[ ] Load Breakout model and train Pong till score = 12 TODO: which layers to train

04.1
---

[ ] Load BreakoutRot and Play Pong

