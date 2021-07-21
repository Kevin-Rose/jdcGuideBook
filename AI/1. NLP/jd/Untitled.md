##### l 项目简介

[副本 Simplified TC-Bot (shimo.im)](https://shimo.im/docs/ic445JcLUiULqAQ0)

##### l DQN agent详细介绍

##### l State Tracker详细介绍

##### l User Simulator及EMC详细介绍

 

简介

Questions:

l 任务型聊天机器人的组成部分是什么？

l 基于强化学习的任务型聊天机器人的需要增加什么模块？

l 任务型聊天机器人的数据应该是什么样的？如果没有真实的多轮对话数据，应该怎么办？

l 在基于强化学习的任务型聊天机器人中，应该如何进行agent的训练？

 

 

 

 

 

##### 对话系统概总

使用强化学习的任务型聊天机器人的对话系统分为三个主要部分。

对话管理器（DM），自然语言理解（NLU）单元和自然语言生成器（NLG）单元。

此外，DM又可分为对话状态跟踪器（state tracker, ST）和agent policy。在大多数情况下，该policy由神经网络表示。另外，整个对话系统循环还包含具有用户目标（user goal）的模拟用户（user simulator）。用户目标代表用户希望从对话中得到什么，如下图，这是饭店预订的例子。

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image002.gif)

在此对话循环中，用户将由NLU组件处理的内容转化为所谓的*语义框架（semantic frame）*，这是agent可以处理的自然语言话语的下层表示。

ST将用户对话动作（语义框架）和当前对话的历史记录处理成状态表示(state representation)，作为agent policy的输入，并还是以语义框架的形式产生动作。还可以查询数据库（DB），以将信息添加到agent action中。

最后，由NLG组件处理该agent action，然后将其转换为自然语言以供用户阅读。

###### MiuLab TC-Bot

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image004.gif)

****

 

用户模拟器和错误模型控制器

****

用户模拟器：基于用户议程（user agenda）建模

错误模型控制器（EMC）：用于在语义框架级别将错误添加到用户模拟器的操作中

 

熟悉数据

**DataBase：**数据库包含具有不同属性的电影票。

它以字典的形式组织，包含request slots（需要去询问对方的信息）以及inform slots（自身已知的可以告知对方的信息）。

以下是一些电影票例子：

{'request_slots': {'date': 'UNK', 'theater': 'UNK'}, 'inform_slots': {'numberofpeople': '4', 'moviename': 'zootopia', 'starttime': 'matinee'}}

{'request_slots': {'theater': 'UNK'}, 'inform_slots': {'city': 'la', 'numberofpeople': '2', 'distanceconstraints': 'downtown', 'video_format': '3d', 'starttime': '7pm', 'date': 'tomorrow', 'moviename': 'creed'}}

{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'city': 'birmingham', 'state': 'al', 'numberofpeople': '2', 'moviename': 'zootopia'}}

{'request_slots': {}, 'inform_slots': {'city': 'seattle', 'numberofpeople': '2', 'theater': 'regal meridian 16', 'starttime': '9:00 pm', 'date': 'tomorrow', 'moviename': 'spotlight'}}

{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'numberofpeople': '5', 'moviename': 'avengers'}}

 

 

**Database Dictionary:** 键值对的说明字典，其中的键是电影票中可以使用的不同slot，值是每个slot的所有可能值的列表。

以下是一些例子：

'city': ['hamilton', 'manville', 'bridgewater', 'seattle', 'bellevue', 'birmingham', 'san francisco', 'portland', ...]

'theater': ['manville 12 plex', 'amc dine-in theatres bridgewater 7', 'bridgewater', 'every single theatre', ...]

'genre': ['comedy', 'comedies', 'kid', 'action', 'violence', 'superhero', 'romance', 'thriller', 'drama', 'family friendly', ...]

 

**User Goal List:** 用户目标也是以词典列表的形式出现，其中也包含request slots以及inform slots。

该数据库的目标是：让模拟用户以此为目的，模拟与agent的对话，并且让agent最后查找到符合该用户目标的电影票。

例子：

{'request_slots': {'date': 'UNK', 'theater': 'UNK'}, 'inform_slots': {'numberofpeople': '4', 'moviename': 'zootopia', 'starttime': 'matinee'}}

{'request_slots': {'theater': 'UNK'}, 'inform_slots': {'city': 'la', 'numberofpeople': '2', 'distanceconstraints': 'downtown', 'video_format': '3d', 'starttime': '7pm', 'date': 'tomorrow', 'moviename': 'creed'}}

{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'city': 'birmingham', 'state': 'al', 'numberofpeople': '2', 'moviename': 'zootopia'}}

{'request_slots': {}, 'inform_slots': {'city': 'seattle', 'numberofpeople': '2', 'theater': 'regal meridian 16', 'starttime': '9:00 pm', 'date': 'tomorrow', 'moviename': 'spotlight'}}{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'numberofpeople': '5', 'moviename': 'avengers'}}

 

什么是一个action

****

一个动作包含一个intent，request slots以及inform slots，示例： 

{'intent': 'request', 'inform_slots': {'city': 'seattle'}, 'request_slots': {'theater': 'UNK', 'starttime': 'UNK'}}

{'intent': 'inform', 'inform_slots': {'moviename': 'the witch'}, 'request_slots': {}}

{'intent': 'done', 'inform_slots': {}, 'request_slots': {}}

{'intent': 'request', 'inform_slots': {}, 'request_slots': {'moviename': 'UNK'}}

{'intent': 'thanks', 'inform_slots': {}, 'request_slots': {'theater': 'UNK'}}

 

都有哪些Intents？

l Inform

l Request

l Thanks

l Match Found

l Reject

l Done

 

如何训练Agent

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

 

此图表示训练中的一轮完整循环的流程。 该系统的四个主要部分是： Agent，对话状态追踪器ST，用户模拟器 User sim 和EMC。

****

 

def run_round(state, warmup=False):

​     \# 1) Agent takes action given state tracker's representation of dialogue (state)

​     agent_action_index, agent_action = dqn_agent.get_action(state, use_rule=warmup)

​     \# 2) Update state tracker with the agent's action

​     round_num = state_tracker.update_state_agent(agent_action)

​     \# 3) User takes action given agent action

​     user_action, reward, done, success = user.step(agent_action, round_num)

​     if not done:

​       \# 4) Infuse error into semantic frame level of user action

​       emc.infuse_error(user_action)

​     \# 5) Update state tracker with user action

​     state_tracker.update_state_user(user_action)

​     \# 6) Get next state and add experience

​     next_state = state_tracker.get_state(done)

​     dqn_agent.add_experience(state, agent_action_index, reward, next_state, done)

​     return next_state, reward, done, success

 

****

 

如何训练agent? 文件代码train.py

\1.   加载数据库数据

\2.   创建对象

\3.    warmup_run()

\4.    train_run()

Warm-up the Agent

def warmup_run():

​    total_step = 0

​    while total_step != WARMUP_MEM and not dqn_agent.is_memory_full():

​      \# Reset episode

​      episode_reset()

​      done = False

​      \# Get initial state from state tracker

​      state = state_tracker.get_state()

​      while not done:

​        next_state, _, done, _ = run_round(state, warmup=True)

​        total_step += 1

​        state = next_state

 

外部循环（一个个对话任务，episode）：在WARMUP_MEM未达到上限或者其经验池完未满之前运行

内部循环（一个个对话回合，round）：done是false之前运行

主要目的：在初始阶段填充经验池。

Train the Agent

 def train_run():

​    episode = 0

​    period_success_total = 0

​    success_rate_best = 0.0

​    \# Almost exact same loop as warm-up -----

​    while episode < NUM_EP_TRAIN:

​      episode_reset()

​      episode += 1

​      done = False

​      state = state_tracker.get_state()

​      while not done:

​        next_state, reward, done, success = run_round(state)

​        period_reward_total += reward

​        state = next_state

​      \# ------

​      period_success_total += success

​      \# Train block ----

​      if episode % TRAIN_FREQ == 0:

​       \# Get success rate

​       success_rate = period_success_total / TRAIN_FREQ

​       \# 1. Empty memory buffer if statemement is true

​       if success_rate >= success_rate_best and success_rate >= SUCCESS_RATE_THRESHOLD:

​         dqn_agent.empty_memory()

​         success_rate_best = success_rate

​       \# Refresh period success total

​       period_success_total = 0

​       \# 2. Copy weights

​       dqn_agent.copy()

​       \# 3. Train weights

​       dqn_agent.train()

 

忽略一些其他变量，以上两者几乎相同。主要区别是，经验池的填充规则以及agent的模型训练。

****

总结

训练文件代码train.py

\1.   加载数据库数据

\2.   创建对象

\3.    warmup_run()

\4.    train_run()

这就是使用DRL训练的GO聊天机器人的主要过程。

 

 

 

 

 

 

DQN Agent

Questions:

l agent的输入是什么？

l agent的输出是什么？

l agent的训练数据是什么？

l 在初始时期，agent如果采取较靠谱的action?

 

 

 

 

 

 

 

agent的目的是什么？

面向目标（GO）聊天机器人的目的是接受训练，以熟练地与实际用户交谈，以完成目标，例如在这里，即查找符合用户条件的电影票。

agent的目标：基于输入的状态产生最合适的动作。

训练方式：Deep Q Learning(DQN)

 

agent的对话配置:agent的action如何表示？

agent使用的对话配置dialogue_config.py ： 

agent所有可能的inform slots、request slots以及结合intents的所有可能actions.

\# Possible inform and request slots for the agent

agent_inform_slots = ['moviename', 'theater', 'starttime', 'date', 'genre', 'state', 'city', 'zip', 'critic_rating',

​          'mpaa_rating', 'distanceconstraints', 'video_format', 'theater_chain', 'price', 'actor',

​          'description', 'other', 'numberofkids']

agent_request_slots = ['moviename', 'theater', 'starttime', 'date', 'numberofpeople', 'genre', 'state', 'city', 'zip',

​           'critic_rating', 'mpaa_rating', 'distanceconstraints', 'video_format', 'theater_chain', 'price',

​           'actor', 'description', 'other', 'numberofkids']

 

\# Possible actions for agent

agent_actions = [

 {'intent': 'done', 'inform_slots': {}, 'request_slots': {}}, # Triggers closing of conversation

 {'intent': 'match_found', 'inform_slots': {}, 'request_slots': {}}

]

for slot in agent_inform_slots:

 agent_actions.append({'intent': 'inform', 'inform_slots': {slot: 'PLACEHOLDER'}, 'request_slots': {}})

for slot in agent_request_slots:

 agent_actions.append({'intent': 'request', 'inform_slots': {}, 'request_slots': {slot: 'UNK'}})

 

\# Rule-based policy request list

rule_requests = ['moviename', 'starttime', 'city', 'date', 'theater', 'numberofpeople']

\# These are possible inform slot keys that cannot be used to query

no_query_keys = ['numberofpeople', usersim_default_key]

agent_inform_slots是agent告知信息的所有可能的键。agent_request_slots是agent请求信息的所有可能的键。

 

神经网络模型

使用Keras构建agent模型。该模型是单隐藏层神经网络。

def _build_model(self):

 model = Sequential()

 model.add(Dense(self.hidden_size, input_dim=self.state_size, activation='relu'))

 model.add(Dense(self.num_actions, activation='linear'))

 model.compile(loss='mse', optimizer=Adam(lr=self.lr))

 return model

 

该代码段中的实例变量给来自 constants.json 

 

Agent Policy：在强化学习的框架下，agent如何采取action ?

**get_action****函数**

l 基于规则（热身阶段）

l 基于神经网络

l 随机选取行为的机制（使得agent探索更多的可能，不局限于已有的经验）

 

def get_action(self, state, use_rule=False):

​     \# self.eps is initialized to the starting epsilon and does NOT get annealed

​     if self.eps > random.random():

​       index = random.randint(0, self.num_actions - 1)

​       \# self._map_index_to_action(index) takes an index and maps the action from all possible agent actions

​       action = self._map_index_to_action(index)

​       return index, action

​     else:

​       if use_rule:

​         return self._rule_action()

​       else:

​         return self._dqn_action(state)

 

 

Rule-Based Policy

在预热期间，将使用基于规则的简单策略。

首先请注意agent的重置方法，该方法仅用于重置此基于规则的策略的几个变量：

def reset(self):

​     self.rule_current_slot_index = 0

​     self.rule_phase = 'not done'

 

策略规则（较粗暴，以agent为导向）：不断请求request slots列表中的下一个slot，直到没有更多slot，然后采取找到匹配操作，最后在最后一轮完成操作。

 

def _rule_action(self):

​     \# self.rule_current_slot_index points to current slot

​     \# rule_requests defined in dialogue_config.py

​     if self.rule_current_slot_index < len(rule_requests):

​       slot = rule_requests[self.rule_current_slot_index]

​       self.rule_current_slot_index += 1

​       rule_response = {'intent': 'request', 'inform_slots': {}, 'request_slots': {slot: 'UNK'}}

​     \# self.rule_phase used to indicate if we are at second to last round or last round

​     elif self.rule_phase == 'not done':

​       rule_response = {'intent': 'match_found', 'inform_slots': {}, 'request_slots': {}}

​       self.rule_phase = 'done'

​     elif self.rule_phase == 'done':

​       rule_response = {'intent': 'done', 'inform_slots': {}, 'request_slots': {}}

​     else:

​       raise Exception('Should not have reached this clause')

​     \# self._map_action_to_index(rule_response) takes an action and gets its index from all possible agent actions

​     index = self._map_action_to_index(rule_response)

​     return index, rule_response

这是使用此简单策略的单个episode的示例：

For example, say rule_requests = ['moviename', 'starttime', 'city'], length: 3

   

Round 1:

rule_current_slot_index = 0 (< 3)

​         |

[request 'moviename', request 'starttime', request 'city', mach_found, done]

   

Round 2:

​            rule_current_slot_index = 1 (< 3)

​                  |

[request 'moviename', request 'starttime', request 'city', mach_found, done]

   

Round 3:

​                    rule_current_slot_index = 2 (< 3)

​                            |

[request 'moviename', request 'starttime', request 'city', mach_found, done]

   

Round 4:

​                         rule_phase = 'not done'

​                                 |

[request 'moviename', request 'starttime', request 'city', mach_found, done]

 

Round 5, final:  

​                          rule_phase = 'done' 

​                                  |                                     

[request'moviename',request'starttime',request'city',mach_found, done]

 

DQN Policy

在训练期间使用：

def _dqn_action(self, state):

​     \# self.beh_model is our keras behavior model

​     index = np.argmax(self.beh_model.predict(state.reshape(1, self.state_size), target=target).flatten())

​     action = self._map_index_to_action(index)

​     return index, action

 

训练方法

dqn_agent.train()在训练过程中，随机获取记忆池中的经验数据（五元组）进行训练。

五元组：s, a, r, s_, d

\# Take a look at the rest of the agent code in dqn_agent.py from the repo!

def train(self):

 \# Calc. num of batches to run

 num_batches = len(self.memory) // self.batch_size

 for b in range(num_batches):

  batch = random.sample(self.memory, self.batch_size)

  states = np.array([sample[0] for sample in batch])

  next_states = np.array([sample[3] for sample in batch])

  beh_state_preds = self._dqn_predict(states) # For leveling error

  \# vanilla means use a DQN, not vanilla means use a Double DQN; vanilla in constants.json

  if not self.vanilla:

​    beh_next_states_preds = self._dqn_predict(next_states) # For indexing for DDQN

  tar_next_state_preds = self._dqn_predict(next_states, target=True) # For target value for DQN (& DDQN)

  inputs = np.zeros((self.batch_size, self.state_size))

  targets = np.zeros((self.batch_size, self.num_actions))

  for i, (s, a, r, s_, d) in enumerate(batch):

​    t = beh_state_preds[i]

​    if not self.vanilla:

​      t[a] = r + self.gamma * tar_next_state_preds[i][np.argmax(beh_next_states_preds[i])] * (not d)

​    else:

​      t[a] = r + self.gamma * np.amax(tar_next_state_preds[i]) * (not d)

​    inputs[i] = s

​    targets[i] = t

  self.beh_model.fit(inputs, targets, epochs=1, verbose=0)

  

 

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image008.gif)

DQN学习资料：

https://www.baidu.com/link?url=QDoWeEF6MJs6gbjL8j3lePqyvAi-I4MdFvz--3r67rE5N5yvWxaXoeKx5qBfXweRv7j1sADlTGaqQO47i_C19K&wd=&eqid=c5f733b400006ca1000000065f87f344

 

 

 

 

 

 

 Dialogue State Tracker对话状态追踪器

Questions:

l ST要追踪哪些状态？如何表示状态？

l ST应该包含哪些功能函数？

l 什么情况下，ST需要与数据库交互？

 

 

 

 

 

 

对话状态跟踪器（ST）是干嘛的？

面向目标的对话系统中的对话状态跟踪器（ST）的主要工作是为agent准备状态。agent需要接收到一个有代表性的状态，以便能做出良好的操作选择。

ST的功能：

l ST通过收集user和agent采取的行动来更新其内部对话历史记录history。

l 记录当前episode中当前的信息进程current informs。

l 为agent提供每一次的输入状态：由当前历史记录和当前状态组成的特征向量。

 

ST中都有哪些信息？

¡ current_informs：当前对话中的共知信息

¡ history

¡ round_num

 

reset

重置所有信息，用于新一个episode的开始： 

def reset(self):

 self.current_informs = {}

 self.history = []

 self.round_num = 0

 

根据当前的对话变化，维护信息（update方法）

对于agent和user sim而言，具备不同的action类型，所以分别需要两个update方法

\# Agent action examples:

{'intent': 'request', 'inform_slots': {}, 'request_slots': {'theater': 'UNK'}}

{'intent': 'inform', 'inform_slots': {'moviename': 'the witch'}, 'request_slots': {}}

{'intent': 'done', 'inform_slots': {}, 'request_slots': {}}

 

\# User action examples:

{'intent': 'request', 'inform_slots': {'city': 'seattle'}, 'request_slots': {'theater': 'UNK', 'starttime': 'UNK'}}

{'intent': 'inform', 'inform_slots': {'moviename': 'the witch'}, 'request_slots': {}}

{'intent': 'done', 'inform_slots': {}, 'request_slots': {}}

{'intent': 'request', 'inform_slots': {}, 'request_slots': {'moviename': 'UNK'}}

{'intent': 'thanks', 'inform_slots': {}, 'request_slots': {'theater': 'UNK'}}

 

Updating with the User Action

\1.   使用action中的inform slots更新current informs

\2.   将action添加到历史记录

\3.   轮数增加

def update_state_user(self, user_action):

​     \# 1)

​     for key, value in user_action['inform_slots'].items():

​       self.current_informs[key] = value

​     \# 2)

​     self.history.append(user_action)

​     \# 3)

​     self.round_num += 1

 

Updating with the Agent Action

*特别地，当agent是行为*‘inform’*和*‘match_found’*时，需要与数据库存进行交互，以特定方式处理。*

 

**处理** ‘inform’

\1.   通过查询database填充inform slot

\2.   更新current informs

 

**处理** ‘match_found’

\1.   从数据库中获取一系列匹配的电影票

\2.   任意取其中一张，利用电影票信息更新agent action的inform slots；另外self.match_key，设置为此票的ID

\3.   如果没有匹配的电影票， self.match_key = ‘no match available’

\4.   更新current informs

 

*成功查询到匹配项*操作的示例：{'intent': 'match_found', 'inform_slots': {'ticket': 24L, 'moviename': 'zootopia', 'theater': 'carmike 16', 'city': 'washington'}, 'request_slots': {}}

*查询匹配操作失败的*示例：{'intent': 'match_found', 'inform_slots': {'ticket': ‘no match available’}, 'request_slots': {}}

 

def update_state_agent(self, agent_action):

​     \# Handle 'inform':

​     if agent_action['intent'] == 'inform':

​       \# 1) Note: db_helper is an object of class DBQuery 

​       inform_slots = self.db_helper.fill_inform_slot(agent_action['inform_slots'], self.current_informs)

​       agent_action['inform_slots'] = inform_slots

​       key, value = list(agent_action['inform_slots'].items())[0] # Only one

​       \# 2)

​       self.current_informs[key] = value

​     \# Handle 'match_found':

​     elif agent_action['intent'] == 'match_found':

​       \# 1) 

​       db_results = self.db_helper.get_db_results(self.current_informs)

​       \# 2)

​       if db_results:

​         \# Arbitrarily pick the first value of the dict

​         key, value = list(db_results.items())[0]

​         agent_action['inform_slots'] = copy.deepcopy(value)

​         agent_action['inform_slots'][self.match_key] = str(key)

​       \# 3)

​       else:

​         agent_action['inform_slots'][self.match_key] = 'no match available'

​       \# 4)

​       self.current_informs[self.match_key] = agent_action['inform_slots'][self.match_key]

​     \# Add round number

​     agent_action.update({'round': self.round_num})

​     \# Add to history

​     self.history.append(agent_action)

 

 

State Preparation

ST另一个重要的工作：为agent提供当前的状态表示。

相关函数为： get_state(self, done)

状态由有关episode状态的有用信息组成：

l 最近的用户操作和最近的agent操作

l round_num，也就是回合数据，可以让agent知道对话的紧迫性（例，如果episode接近其允许的最大回合数，agent可以考虑采取match found的动作） 

l current informs的信息

l 数据库中有多少项与这些current informs匹配的信息

 

def get_state(self, done=False):

​     \# If done then fill state with zeros

​     if done:

​       return self.none_state

​     user_action = self.history[-1]

​     \# Get database info that is useful for the agent

​     db_results_dict = self.db_helper.get_db_results_for_slots(self.current_informs)

​     last_agent_action = self.history[-2] if len(self.history) > 1 else None

​     \# Create one-hot of intents to represent the current user action

​     \# self.num_intents is the total number of all different intents defined in dialogue_config.py

​     user_act_rep = np.zeros((self.num_intents,))

​     \# self.intents_dict is a dict with keys of intents and values of their index in the list of intents

​     user_act_rep[self.intents_dict[user_action['intent']]] = 1.0

​     \# Create bag of inform slots representation to represent the current user action

​     \# self.num_slots is the total number of different slots defined in dialogue_config

​     user_inform_slots_rep = np.zeros((self.num_slots,))

​     for key in user_action['inform_slots'].keys():

​       \# self.slots_dict is like self.intents_dict except with slots

​       user_inform_slots_rep[self.slots_dict[key]] = 1.0

​     \# Create bag of request slots representation to represent the current user action

​     user_request_slots_rep = np.zeros((self.num_slots,))

​     for key in user_action['request_slots'].keys():

​       user_request_slots_rep[self.slots_dict[key]] = 1.0

​     \# Create bag of filled_in slots based on the current_slots

​     current_slots_rep = np.zeros((self.num_slots,))

​     for key in self.current_informs:

​       current_slots_rep[self.slots_dict[key]] = 1.0

​     \# Encode last agent intent

​     agent_act_rep = np.zeros((self.num_intents,))

​     if last_agent_action:

​      agent_act_rep[self.intents_dict[last_agent_action['intent']]] = 1.0

​     \# Encode last agent inform slots

​     agent_inform_slots_rep = np.zeros((self.num_slots,))

​     if last_agent_action:

​       for key in last_agent_action['inform_slots'].keys():

​         agent_inform_slots_rep[self.slots_dict[key]] = 1.0

​     \# Encode last agent request slots

​     agent_request_slots_rep = np.zeros((self.num_slots,))

​     \# If not start of episode

​     if last_agent_action:

​       for key in last_agent_action['request_slots'].keys():

​         agent_request_slots_rep[self.slots_dict[key]] = 1.0

​     \# Value representation of the round num

​     turn_rep = np.zeros((1,)) + self.round_num / 5.

​     \# One-hot representation of the round num

​     turn_onehot_rep = np.zeros((self.max_round_num,))

​     turn_onehot_rep[self.round_num - 1] = 1.0

​     \# Representation of DB query results (scaled counts)

​     kb_count_rep = np.zeros((self.num_slots + 1,)) + db_results_dict['matching_all_constraints'] / 100.

​     for key in db_results_dict.keys():

​       if key in self.slots_dict:

​         kb_count_rep[self.slots_dict[key]] = db_results_dict[key] / 100.

​     \# Representation of DB query results (binary)

​     kb_binary_rep = np.zeros((self.num_slots + 1,)) + np.sum(db_results_dict['matching_all_constraints'] > 0.)

​     for key in db_results_dict.keys():

​       if key in self.slots_dict:

​         kb_binary_rep[self.slots_dict[key]] = np.sum(db_results_dict[key] > 0.)

​     state_representation = np.hstack(

​       [user_act_rep, user_inform_slots_rep, user_request_slots_rep, agent_act_rep, agent_inform_slots_rep,

​       agent_request_slots_rep, current_slots_rep, turn_rep, turn_onehot_rep, kb_binary_rep,

​       kb_count_rep]).flatten()

​     return state_representation

 

状态跟踪有很多相关研究工作，例如对信息进行编码的最佳方法以及在状态中提供哪些信息效果更好。

当前这种状态的表示可能并非最佳，但需要大量调整才能优化此过程。

 

query系统

在之前已知，状态跟踪器ST遇到agent action是inform以及match found时，需要查询数据库以获取相关信息。

这里主要介绍，db_query.py中的一些方法。

 

根据条件获取数据库结果

get_db_results(constraints) -> dict：

在agent action是match found时会被调用，根据constraints, 逐个查看数据库中的每个项目，找到数据库中的所有匹配项。

假设数据库如下所示：

{0: {'theater': 'regal 6', 'date': 'tonight', 'city': 'seattle'},

1: {'date': 'tomorrow', 'city': 'seattle'},

2: {'theater': 'regal 6', 'city': 'washington'}}

约束是： {'theater': 'regal 6', 'city': 'seattle'}

输出将是{0: {'theater': 'regal 6', 'date': 'tonight', 'city': 'seattle'}}

 

填写通知槽inform slot：当有多个匹配的电影票时，如何填写agent action中的inform slot？（真实情境中应该是多选）

fill_inform_slot(inform_slot_to_fill, current_inform_slots) -> dict：

在agent action是inform时会被调用，首先调用get_db_results(current_informs)获取所有数据库匹配电影票之后，根据inform_slot_to_fill 返回出现的最高频者对应的value。

例如，假设这些是从返回的匹配项get_db_results(constraints)：

{2: {'theater': 'regal 6', 'date': 'tomorrow', 'moviename': 'zootopia'},

45 : {'theater': 'amc 12', 'date': 'today'},

67: {'theater': 'regal 6', 'date': 'after tomorrow'}}

如果inform_slot_to_fill是'theater'，此方法将返回{'theater': 'regal 6'}

如果inform_slot_to_fill是'date'，输出将为{'date': 'tomorrow'}

 

获取有关slot的相关数据库统计结果，作为状态输出的一部分

get_db_results_for_slots(current_informs) -> dict：

在获取stateget_state(self, done=false)时会调用，根据current informs 遍历整个数据库,统计相关信息。

例如，数据库如下：

{0: {theater: regal 6, date: tonight, city: seattle},

1: {date: tomorrow, city: seattle},

2: {theater: regal 6, city: washington}}

如果current informs 是：{'theater': 'regal 6', 'city': 'washington'}

输出将是{'theater': 2, 'city': 1, 'matching_all_constraints': 1}

因为两个数据库项具有‘theater’: ‘regal 6’，一个数据库项具有‘city': 'washington’，并且一个数据库项匹配所有约束（2）。

 

总结 

状态追踪器ST使用每个agent和user action来更新它的历史和current informs，基于此它可以为agent准备一个最有代表性的信息状态。

另外，在某些情况下，它还需要使用简单的查询系统来补充更多的信息。

 

 

 

 

 

User Simulator and Error Model Controller

Questions:

l 用户模拟器的作用是什么？

l 用户模拟器如何设计？需要数据吗？需要有记忆吗？

l 用户模拟器需要与数据库交互吗？

l EMC的作用是什么？

 

 

 

 

 

 

 

 

 

注：本部分重点介绍的两个文件是user_simulator.py和error_model_controller.py。 

 

用户模拟器User Simulator

用户模拟器用于模拟实际用户，因此与强迫真实用户坐下来进行多个小时的人机互动相比，可以更快地训练agent。针对聊天机器人域的用户模拟器研究是一个热门研究方向。

 

****

 

什么是用户目标User Goal？

l 每个目标都由通知槽inform slots和请求槽request slots组成，就像一个对话动作一样，区别是其没有意图。

l 用户目标的通知槽inform slots表示模拟用户对于电影票的约束条件。

l 请求槽request slots模拟用户获得有关满足条件的票的相关信息（注意这里不会对出票结果产生影响）。

l 该系统与真实用户之间的主要区别在于，用户在了解有关可用票证的更多信息时可能会改变主意。但是在这里不会发生这种情况*！*

l 最后，当用户目标中的所有slots被填充时，表明成功完成一个episode。

一些用户目标示例：

{'request_slots': {'date': 'UNK', 'theater': 'UNK'}, 'inform_slots': {'numberofpeople': '4', 'moviename': 'zootopia', 'starttime': 'matinee'}}

{'request_slots': {'theater': 'UNK'}, 'inform_slots': {'city': 'la', 'numberofpeople': '2', 'distanceconstraints': 'downtown', 'video_format': '3d', 'starttime': '7pm', 'date': 'tomorrow', 'moviename': 'creed'}}

{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'city': 'birmingham', 'state': 'al', 'numberofpeople': '2', 'moviename': 'zootopia'}}

{'request_slots': {}, 'inform_slots': {'city': 'seattle', 'numberofpeople': '2', 'theater': 'regal meridian 16', 'starttime': '9:00 pm', 'date': 'tomorrow', 'moviename': 'spotlight'}}{'request_slots': {'date': 'UNK', 'theater': 'UNK', 'starttime': 'UNK'}, 'inform_slots': {'numberofpeople': '5', 'moviename': 'avengers'}}

 

用户模拟器内部状态User Simulator Internal State

用户模拟器的内部状态（与状态跟踪器ST的状态不同）既跟踪目标slots，又跟踪当前会话的历史记录。它用于产生用户动作。具体来说，此状态的构成如下：

l rest slots：所有未被填充的slots

l history slots：至今所有被提到过的inform slots

l request slots：用户希望在近期操作中执行的request slots

l inform slots：agent在当前正在执行的操作中的inform slots

l intent：当前动作的目的

 

用户模拟器动作User Simulator Actions

与可能的agent action相比，用户可以采取的动作更加多样化，有时甚至更为复杂：一个用户操作可以具有多个请求槽request slots或多个通知槽inform slots。另外，它还可以在某些情况下（例如初始操作）同时包含两种槽。

 

用户sim对话配置

以下是用户sim中的对话配置dialogue_config.py： 

\# Used in EMC for intent error (and in user)

usersim_intents = ['inform', 'request', 'thanks', 'reject', 'done']

\# The goal of the agent is to inform a match for this key

usersim_default_key = 'ticket'

\# Required to be in the first action in inform slots of the usersim if they exist in the goal inform slots

usersim_required_init_inform_keys = ['moviename']

 

Reset用户状态

用户状态的重置很重要，因为它会选择新的用户目标，重置状态并返回初始操作。

\1.   随机选择一个目标

\2.   将默认slots添加到目标

\3.   清除状态的所有内容

\4.   将所有slots添加到‘rest_slots’

\5.   初始化对话状态（FAIL）

\6.   初始化动作

def reset(self):

​     \# 1)

​     self.goal = random.choice(self.goal_list)

​     \# 2)

​     self.goal['request_slots'][self.default_key] = 'UNK'

​     \# 3)

​     self.state = {}

​     self.state['history_slots'] = {}

​     self.state['inform_slots'] = {}

​     self.state['request_slots'] = {}

​     self.state['rest_slots'] = {}

​     \# 4)

​     self.state['rest_slots'].update(self.goal['inform_slots'])

​     self.state['rest_slots'].update(self.goal['request_slots'])

​     self.state['intent'] = ''

​     \# 5) Can be set to SUCCESS in response to match found, init. to failure

​     self.constraint_check = FAIL

​     \# 6)

​     return self._return_init_action()

 

初始用户操作

\1.   初始操作必须始终是一个请求

\2.   它还必须始终包含dialogue_config.py 中usersim_required_init_inform_keys定义的所有inform slots。在这里，‘moviename’始终会在初始操作中作为用户的inform slot

\3.   必须包含来自目标的一个随机request slot

def _return_init_action(self):

​     \# 1)

​     self.state['intent'] = 'request'

​     \# 2)

​     if self.goal['inform_slots']:

​       \# Pick all the required init. informs, and add if they exist in goal inform slots

​       for inform_key in usersim_required_init_inform_keys:

​         if inform_key in self.goal['inform_slots']:

​           self.state['inform_slots'][inform_key] = self.goal['inform_slots'][inform_key]

​           \# Must remove from rest slots and add to history as described below in requirements (req. #3) section

​           self.state['rest_slots'].pop(inform_key)

​           self.state['history_slots'][inform_key] = self.goal['inform_slots'][inform_key]

​     \# 3)

​     \# Remove ticket slot

​     self.goal['request_slots'].pop(self.default_key)

​     \# If there are still other requests after ticket was removed then pick a random one

​     if self.goal['request_slots']:

​       req_key = random.choice(list(self.goal['request_slots'].keys()))

​     else:

​     \# If its empty now after removing ticket, then just add ticket

​       req_key = self.default_key

​     \# Make sure to add ticket back to goal

​     self.goal['request_slots'][self.default_key] = 'UNK'

​     \# And of course add the selected req. to the state

​     self.state['request_slots'][req_key] = 'UNK'

​     user_response = {}

​     user_response['intent'] = self.state['intent']

​     user_response['request_slots'] = copy.deepcopy(self.state['request_slots'])

​     user_response['inform_slots'] = copy.deepcopy(self.state['inform_slots'])

​     return user_response

 

 

step方法

**step方法的输入是agent action，输出是user action，reward, done, if success。**

特别地：

\1.   清除状态中之前的inform slots和intent，因为它们需要根据当前的情况进行更新

\2.   如果回合等于最大回合数，则intent为‘done’并设置success = FAIL

\3.   否则，根据agent action的意图来制定动作

\4.   制作用户动作

\5.   计算该步骤的标量奖励

\6.   返回user action，reward, done, if success

 

def step(self, agent_action):

​     \# 1)

​     self.state['inform_slots'].clear()

​     self.state['intent'] = ''

​     done = False

​     success = NO_OUTCOME

​     \# 2) 'round' is added to agent action in the agent action update method of the state tracker

​     if agent_action['round'] == self.max_round:

​       done = True

​       success = FAIL

​       self.state['intent'] = 'done'

​       self.state['request_slots'].clear()

​     \# 3)

​     else:

​       agent_intent = agent_action['intent']

​       if agent_intent == 'request':

​         self._response_to_request(agent_action)

​       elif agent_intent == 'inform':

​         self._response_to_inform(agent_action)

​       elif agent_intent == 'match_found':

​         self._response_to_match_found(agent_action)

​      \# 3.a)

​       elif agent_intent == 'done':

​         success = self._response_to_done()

​         self.state['intent'] = 'done'

​         self.state['request_slots'].clear()

​         done = True

​     \# 4)

​     user_response = {}

​     user_response['intent'] = self.state['intent']

​     user_response['request_slots'] = copy.deepcopy(self.state['request_slots'])

​     user_response['inform_slots'] = copy.deepcopy(self.state['inform_slots'])

​     \# 5)

​     reward = reward_function(success, self.max_round)

​     \# 6)

​     return user_response, reward, done, True if success is 1 else False

 

奖励函数

在每个回合都会-1，希望agent高效地对话，最后根据结果会有相应的比较大的鼓励或者惩罚。

 

def reward_function(success, max_round):

​     \# Starts with -1 because we want to penalize every step so the agent learns to succeed quicker

​     reward = -1

​     \# If FAIL then return -1 + -max_round

​     if success == FAIL:

​       reward += -max_round

​     \# If SUCCESS then return -1 + 2 * max_round

​     elif success == SUCCESS:

​       reward += 2 * max_round

​     \# NO_OUTCOME so just return -1

​     return reward

 

回应类型Types of Responses

一些响应规则很复杂，或者看起来有些武断。但是*请记住制作响应的许多规则都很复杂，因此用户sim才可能更加地人性化，这将有助于代理与实际用户打交道。* 

 

几个用户回应中的规则Requirement：

\1.   如果用户意图是‘inform’则必须有通知插槽，但不能有请求插槽，以免与下面的要求2冲突

\2.   如果用户意图是‘request’，它可以*同时具有*通知和请求槽，但必须至少具有请求槽：这是一个复杂的操作，其目的是向请求中添加信息以使其更加人性化

\3.   不管是agent操作还是用户操作包含通知槽时，都必须从rest slots中删除该通知槽，并更新history slots（表明这些信息已经共知了）

\4.   每当agent操作包含通知槽时，都必须将其从user sim的状态request slots中移除（表明agent已经回答了这个问题）

 

回应：request

分为4种主要情况：

1）如果agent requests在目标中有对应的inform slots尚未通知，则从目标中取对应的值进行通知

2）如果agent requests在目标中有对应的inform slots并且已经被告知，则从历史记录中取对应的值进行通知

3）如果agent requests在目标中有对应的request slots并且没被告知，则用户也request同一个slot并且随机发出一个inform slot

4）否则，说明用户sim不在乎agent所请求的槽，告知‘anything’

 

def _response_to_request(self, agent_action):

​     agent_request_key = list(agent_action['request_slots'].keys())[0]

​     \# Case 1)

​     if agent_request_key in self.goal['inform_slots']:

​       self.state['intent'] = 'inform'

​       self.state['inform_slots'][agent_request_key] = self.goal['inform_slots'][agent_request_key]

​       \# Requirement 1)

​       self.state['request_slots'].clear()

​       \# Requirement 3)

​       self.state['rest_slots'].pop(agent_request_key, None)

​       self.state['history_slots'][agent_request_key] = self.goal['inform_slots'][agent_request_key]

​     \# Case 2)

​     elif agent_request_key in self.goal['request_slots'] and agent_request_key in self.state['history_slots']:

​       self.state['intent'] = 'inform'

​       self.state['inform_slots'][agent_request_key] = self.state['history_slots'][agent_request_key]

​       \# Requirement 1)

​       self.state['request_slots'].clear()

​     \# Case 3)

​     elif agent_request_key in self.goal['request_slots'] and agent_request_key in self.state['rest_slots']:

​       self.state['request_slots'].clear()

​       self.state['intent'] = 'request'

​       self.state['request_slots'][agent_request_key] = 'UNK'

​       \# Requirement 2)

​       rest_informs = {}

​       for key, value in list(self.state['rest_slots'].items()):

​         if value != 'UNK':

​           rest_informs[key] = value

​       if rest_informs:

​         key_choice, value_choice = random.choice(list(rest_informs.items()))

​         self.state['inform_slots'][key_choice] = value_choice

​         \# Requirement 3)

​         self.state['rest_slots'].pop(key_choice)

​         self.state['history_slots'][key_choice] = value_choice

​     \# Case 4)

​     else:

​       self.state['intent'] = 'inform'

​       self.state['inform_slots'][agent_request_key] = 'anything'

​       \# Requirement 1)

​       self.state['request_slots'].clear()

​       \# Requirement 3) However, dont need to remove from rest because it won't be in rest

​       self.state['history_slots'][agent_request_key] = 'anything'

 

 

回应：Inform

2个主要的回应案例：

1）如果agent通知了目标中的某些内容，并且不匹配，则通知正确的值

2）否则，请选择一些slot进行请求或通知

a）如果有request slots，则从中发出请求

b）如果有rest slots，则从中发出请求

c）‘thanks’，实际上意味着“无话可说”

 

def _response_to_inform(self, agent_action):

​     agent_inform_key = list(agent_action['inform_slots'].keys())[0]

​     agent_inform_value = agent_action['inform_slots'][agent_inform_key]

​     \# Requirement 3)

​     self.state['history_slots'][agent_inform_key] = agent_inform_value

​     self.state['rest_slots'].pop(agent_inform_key, None)

​     \# Requirement 4)

​     self.state['request_slots'].pop(agent_inform_key, None)

   

 

​     \# Case 1)

​     if agent_inform_value != self.goal['inform_slots'].get(agent_inform_key, agent_inform_value):

​       self.state['intent'] = 'inform'

​       self.state['inform_slots'][agent_inform_key] = self.goal['inform_slots'][agent_inform_key]

​       \# Requirement 1)

​       self.state['request_slots'].clear()

​       \# Requirement 3) But without removing from rest as it should already be removed from rest

​       self.state['history_slots'][agent_inform_key] = self.goal['inform_slots'][agent_inform_key]

​     \# Case 2)

​     else:

​       \# Case 2.a)

​       if self.state['request_slots']:

​         self.state['intent'] = 'request'

​       \# Case 2.b)

​       elif self.state['rest_slots']:

​        \# Here the ticket is being removed from rest (if it is in there) so that it selects another slot, 

​        \# whether its a request or inform, but if ticket is the only one in rest then just request it

​        def_in = self.state['rest_slots'].pop(self.default_key, False)

​        if self.state['rest_slots']:

​         key, value = random.choice(list(self.state['rest_slots'].items()))

​         if value != 'UNK':

​           self.state['intent'] = 'inform'

​           self.state['inform_slots'][key] = value

​           \# Requirement 3)

​           self.state['rest_slots'].pop(key)

​           self.state['history_slots'][key] = value

​         else:

​           self.state['intent'] = 'request'

​           self.state['request_slots'][key] = 'UNK'

​        else:

​          self.state['intent'] = 'request'

​         self.state['request_slots'][self.default_key] = 'UNK'

​        if def_in == 'UNK':

​         self.state['rest_slots'][self.default_key] = 'UNK'

​      \# Case 2.c)

​      else:

​        self.state['intent'] = 'thanks'

 

如何算“成功”？

对话成功的条件：

l 收到user的‘match_found’并且满足所有目标限制

l ‘match_found’ 之后user采取行动为 ‘done’，并且rest slots为空

 

回应：match found

\1.   有一个实际的匹配电影票ID值，而不是‘no match available’

\2.   来自目标的所有通知槽inform slots都必须在此电影票的属性中

\3.   并且所有属性值匹配

\4.   如果以上条件都满足，self.constraint_check则设置为SUCCESS否则FAIL

l 如果成功匹配，则发出意图‘thanks’和仍处于状态请求中的所有请求槽进行答复

l 否则，发出意图‘reject’

def _response_to_match_found(self, agent_action):

​     agent_informs = agent_action['inform_slots']

​     self.state['intent'] = 'thanks'

​     self.constraint_check = SUCCESS

​     \# Add the ticket slot to history and remove from rest and requests as per requirement 3 and 4

​     self.state['rest_slots'].pop(self.default_key, None)

​     self.state['history_slots'][self.default_key] = str(agent_informs[self.default_key])

​     self.state['request_slots'].pop(self.default_key, None)

​     \# 1)

​     if agent_informs[self.default_key] == 'no match available':

​       self.constraint_check = FAIL

​     \# 2 and 3) 

​     for key, value in self.goal['inform_slots'].items():

​       \# No query indicates slots that cannot be in a ticket so they shouldn’t be checked

​       if key in self.no_query:

​         continue

​       if value != agent_informs.get(key, None):

​         self.constraint_check = FAIL

​         break

​     \# 4)

​     if self.constraint_check == FAIL:

​       self.state['intent'] = 'reject'

​       self.state['request_slots'].clear()

回应：done

返回成功的条件 

1）self.constraint_check必须设置为SUCCESS，表明找到了有效的匹配项

2）rest slots必须为空 

def _response_to_done(self):

​     \# Constraint 1)

​     if self.constraint_check == FAIL:

​       return FAIL

​     \# Constraint 2)

​     if self.state['rest_slots']:

​       return FAIL

​     return SUCCESS

 

错误模型控制器Error Model Controller

在从step函数输出用户操作后，将其发送到错误模型控制器（EMC），在其中注入错误。

在TC-Bot中，发现这样做实际上有助于agent处理现实生活中的真实用户的噪声。EMC会在通知槽和用户操作意图中添加错误。

 

l 通知槽错误：

¡ 随机替换该槽的值

¡ 替换整个槽

¡ 删除该槽

¡ 综合以上三种情况

l 意图错误：

¡ 用随机意图替换原本意图

\# The probability for each slot to be changed

   self.slot_error_prob = constants['emc']['slot_error_prob']

   \# One of the 4 modes for slot level error listed above

   self.slot_error_mode = constants['emc']['slot_error_mode'] # [0, 3]

   \# Probability for randomly selecting new intent

   self.intent_error_prob = constants['emc']['intent_error_prob']

   \# The database dict. from part I, holds all possible slot keys and their respective values

   self.movie_dict = db_dict

   \# List of all possible user sim intents, from dialogue_config.py

   self.intents = usersim_intents

 

   def infuse_error(self, frame):

​     informs_dict = frame['inform_slots']

​     for key in list(frame['inform_slots'].keys()):

​       assert key in self.movie_dict

​       if random.random() < self.slot_error_prob:

​         if self.slot_error_mode == 0: # replace the slot_value only

​           self._slot_value_noise(key, informs_dict)

​         elif self.slot_error_mode == 1: # replace slot and its value

​           self._slot_noise(key, informs_dict)

​         elif self.slot_error_mode == 2: # delete the slot

​           self._slot_remove(key, informs_dict)

​         else: # Combine all three

​           rand_choice = random.random()

​           if rand_choice <= 0.33:

​             self._slot_value_noise(key, informs_dict)

​           elif rand_choice > 0.33 and rand_choice <= 0.66:

​             self._slot_noise(key, informs_dict)

​           else:

​             self._slot_remove(key, informs_dict)

​     if random.random() < self.intent_error_prob: # add noise for intent level

​       frame['intent'] = random.choice(self.intents)

 

   def _slot_value_noise(self, key, informs_dict):

​     informs_dict[key] = random.choice(self.movie_dict[key])

 

   def _slot_noise(self, key, informs_dict):

​     informs_dict.pop(key)

​     random_slot = random.choice(list(self.movie_dict.keys()))

​     informs_dict[random_slot] = random.choice(self.movie_dict[random_slot])

 

   def _slot_remove(self, key, informs_dict):

​     informs_dict.pop(key)

总结

我们在这里创建的用户模拟器使用简单的规则来进行拟人行为。错误模型控制器的目的是更接近真实场景，以提高agent的抗噪能力。

 

训练效果

 

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

 

总结 

****

![图片](file:///C:/Users/KevinLiu/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

 

 