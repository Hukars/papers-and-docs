### Gym Documentation
Gym是一个开发和比较强化学习的工具包。他对于智能体的结构没有任何假设，并且和任何数字计算库兼容，e.g.,TensorFlow.
Gym库一些环境的集合，对应了一系列测试问题。在这些环境里面，你可以去执行你的强化学习算法。这些环境有一个共享的接口，允许你写出通用的代码。

####Environment
```python
import gym
env = gym.make('MountainCar-v0')
env.reset()
for _ in range(1000):
	env.render()
	env.step(env.action_space.sample())
env.close()
```
- reset(): 对于有终止状态的RL问题，一条episode结束后需要重置环境。reset()就是用来在每一次尝试中初始化状态等相关信息的函数
- render(): 图像引擎,显示环境中的物体图像，方便调试代码
- step(): 物理引擎，模拟环境中的物体运动;输入是动作a，输出是**下一步状态，立即回报，是否终止，调试项**

#### Observations
环境的step函数返回了你所需要的信息：
- obervation(object): an environment-specific object representing your observation of the environment.
- reward(float): amount of reward achieved by the previous action.
- done(boolean): whether it’s time to reset the environment again.
- info (dict): diagnostic information useful for debugging.

```python
observation,reward,done,info = env.step(action)
```

####Spaces
每一个环境都有一个action_space和observation_space,他们定义了合法的动作和状态形式。
```python
import gym
env = gym.make('CartPole-v0')
print(env.action_space)
#> Discrete(2)
print(env.observation_space)
#> Box(4,)


print(env.observation_space.high)
#> array([ 2.4       ,         inf,  0.20943951,         inf])
print(env.observation_space.low)
#> array([-2.4       ,        -inf, -0.20943951,        -inf])
```

#### Available Environments
Gym拥有各种环境，从容易到困难，涉及许多不同种类的数据。 查看环境的[完整列表](https://gym.openai.com/envs/#classic_control)以获取鸟瞰图。
- [Classic control](https://gym.openai.com/envs#classic_control)and [toy text](https://gym.openai.com/envs#toy_text):完善的小规模任务，大部分来自RL文献。适用于**入门**。
- [Algorithmic](https://gym.openai.com/envs#algorithmic):执行数字计算任务，通过从例子中来学习！
- [Atari](https://gym.openai.com/envs#atari):来玩经典的Atari游戏吧！
- [2D和3D机器人](https://gym.openai.com/envs#mujoco):在高精度的模拟环境下控制机器人。

为了列举你已经安装的可用环境，只需要调用**gym.envs.registry**：
```python
from gym import envs
print(envs.registry.all())
#> [EnvSpec(DoubleDunk-v0), EnvSpec(InvertedDoublePendulum-v0), EnvSpec(BeamRider-v0), EnvSpec(Phoenix-ram-v0), EnvSpec(Asterix-v0), EnvSpec(TimePilot-v0), EnvSpec(Alien-v0), EnvSpec(Robotank-ram-v0), EnvSpec(CartPole-v0), EnvSpec(Berzerk-v0), EnvSpec(Berzerk-ram-v0), EnvSpec(Gopher-ram-v0), ...
```

#### 总结
Gym的出现为强化学习环境提供了标准化，同时也对高质量的可用环境进行了整理，对于强化学习研究的发展是一种不小的驱动力。
