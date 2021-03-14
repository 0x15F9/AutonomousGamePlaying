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

> 12548: done 474 games, mean reward 0.090, eps 0.87, speed 9.45 f/s max reward 0.3

```
    env = gym.make(env_name)
    env = EpisodicLifeEnv(env)
    env = ClipRewardEnv(env)
    env = MaxAndSkipEnv(env)
    env = FireResetEnv(env)
    env = ProcessFrame84BreakoutRotate(env)
    env = ImageToPyTorch(env)
    env = BufferWrapper(env, 4)
    env = ScaledFloatFrame(env)
```

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

[ ] Train till score = 8 and save model

[ ] Load model and train till score = 12

04
===

From 02, 03

[ ] Load Pong model and train till score = 12 TODO: which layers to train