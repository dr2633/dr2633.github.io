
## Reverse Evaluations: Modeling Reward Functions from User Interaction 

Derek Rosenzweig
10/1/2024

### **Opening Thoughts**

Traditionally, we have assumed that humans are the best evaluators of models—particularly when it comes to assessing key issues like security risks and bias. This approach dominated the early years of model development, where human oversight was considered the gold standard for evaluation. However, as we aim to align increasingly capable systems (those surpassing human expertise in important domains), this assumption is rapidly changing ([Burns et al., 2023](https://cdn.openai.com/papers/weak-to-strong-generalization.pdf)). 

We are entering a phase where models not only exceed human performance but also access and process information beyond the psychophysical limitations of biological sensing. Humans are constrained by the evolutionary endowment of sensory instruments (retina, cochlea, etc.) and the physical limits of biological neural processing (ie. axon diameter and number of dendrites). Not only are we bottlenecked in terms of computational capacity, but we also have inherent limitations in the bandwidth and resolution of information processing. For example, we cannot see ultraviolet light or hear ultrasonic frequencies—we cannot compute with information that we do not have access to.
### **Reversal of Evaluations**

Rather than humans evaluating models, we now exist in a regime where models are conducting the primary evaluations of human users. These models learn to assess preferences, infer reward functions, and analyze user behavior, ultimately shaping human decisions and life trajectories. This dynamic was already a challenge in the early days of the internet and social media—think of [behavioral nudges](https://www.sciencedirect.com/science/article/abs/pii/0167268180900517) popularized by Richard Thaler's work—but the stakes are now much higher.

In the past, the ability to steer user access to information through search algorithms and social media feeds was more straightforward—developers could efficiently and selectively organize and arrange content to drive internet traffic and consumption patterns. Today, however, AI models personalize and optimize these interventions at the individual level, making their influence more pervasive and difficult to steer for audiences at scale.

Richard Thaler offers a compelling analogy for optimal choice architecture:

_"A useful interface for understanding an optimal choice architecture is GPS.  
Decide where you want to go and get the trajectory.  
If you see something else, the system will never complain.  
Each task should be as easy as following directions on GPS."_

Just as a GPS guides us to our destination while allowing the freedom to choose alternate routes, AI models provide personalized pathways intended to optimize our experiences. However, unlike the transparency of a GPS system, these models can subtly influence our decisions without our conscious awareness.

Consider the [regulation infrastructure](https://www.rand.org/pubs/research_briefs/RB1501.html) around the deployment of consumer applications like GPS. These systems are subject to standards that protect user interests and privacy. There remain important lessons for policymakers by reflecting on the overall success of GPS being integrated into our personal and works lives as well as the crucial role in governance. 

The successful integration of GPS into everyday life provides a useful blueprint for policymakers, demonstrating how effective governance can guide the responsible adoption of new technologies. Importantly, many future applications—both known and unforeseen—emerge over time. For example, while GPS regulators likely anticipated use in vehicles, they may not have foreseen that nearly every individual would carry a smartphone with geolocation capabilities.
![[nudge.jpg]]

### Inverse Reinforcement Learning and Learning a User's Reward Functions 

One way to understand these developments is through the lens of Inverse Reinforcement Learning (IRL). IRL allows models to infer reward functions—or underlying motivations—behind human actions by observing user behavior. By determining what drives us, models can predict future actions, tailor recommendations, and influence our choices. For instance, a streaming service might analyze your viewing habits to suggest new content, subtly guiding your entertainment choices. This raises important questions about autonomy, privacy, and the asymmetric balance of information as human users interact with models.

_Note: Readers with strong familiarity with techniques in RL may skip this section._

*For those interested in more, see [Pieter Abbeel's tutorial on IRL](https://people.eecs.berkeley.edu/~pabbeel/cs287-fa12/slides/inverseRL.pdf)*
### **Overview of the IRL Framework**

To understand how IRL models can infer user motivations, let’s break down the framework in more detail:

- **Observed trajectories**: We assume that a user’s behavior can be represented as a set of trajectories, $τ={s1,a1,s2,a2,...,sT}$, where _s_ are states and _a_ are actions taken by the user. In this framework, user actions (like clicks or time spent reviewing content) are responses to the states they find themselves in (their environment or context).
    
- **Policy and reward**: The user's actions are assumed to follow some policy $π(a∣s)$, which is optimal with respect to a hidden reward function R(s) over the state space.
    
- **IRL’s Objective**: Given the observed behavior, IRL tries to find the reward function R that, if maximized by the user, would generate the same behavior (i.e., trajectories) observed.
    

**Mathematical Optimization:** In IRL, you typically solve an optimization problem of the form:

$R∗=arg⁡max⁡R∑τ∈Dlog⁡P(τ∣R)$

Where P(τ∣R) is the probability of observing trajectory τ given a reward function R. The challenge is determining the reward function R∗ that maximizes the likelihood of the observed behavior.
### Challenges in Extracting Reward Functions from User Interaction

Extracting reward functions from user interaction involves observing behavior across multiple dimensions and timescales. Every click, choice, or interaction a user makes can be seen as a signal about their preferences and motivations. Models synthesize these signals, finding patterns that might even be imperceptible to the user themselves. They can then weigh these interactions against known outcomes—success in tasks, satisfaction with recommendations, long-term user engagement—and adjust their internal reward representations accordingly.

However, there are significant challenges. Reward functions can be unstable, context-dependent, and dynamic. What a user values today may differ dramatically from what they value tomorrow. 

The risk here is that models might overfit to short-term preferences, optimizing for immediate engagement rather than long-term goals. To overcome this, models need to be sensitive to longer-term feedback loops—understanding not just how to satisfy a user's current needs but how to guide them toward better outcomes, even when that might involve discomfort or uncertainty in the present.

### **Opportunities for Research: Duration and Depth of User Engagement**

**Time spent reviewing outputs**: The amount of time the user spends reading or engaging with a generated response is an implicit action reflecting their interest or attention.

An interesting area for further research is the use of advanced metrics to model reward functions based on user engagement with language models. For instance, time spent reviewing content provides a subtle but important signal of user interest. By analyzing this data, models could infer deeper preferences, especially when users do not interact in explicit ways.

**User Engagement Model:** One potential approach is to formalize a composite engagement score that balances different interaction signals:

$E = f(T_r, R_e, Q_d)$

Where:

- $T_r$ is the time spent reviewing the content,
- $R_e$ is the frequency of re-engagement with the same or similar content,
- $Q_d$ is query depth, such as rephrasing, asking for clarifications, or exploring alternative answers.

**Personalization and User Attention**

Research in this area could help improve personalized recommendations, by learning when and why certain content captures user attention. It could refine models for surfacing more relevant or engaging content, thereby enhancing user satisfaction over time.

**Balancing Short-Term vs. Long-Term Goals**

By studying patterns of attention across different time spans, models can better infer not just short-term engagement (e.g., quickly skimming headlines) but also how long-term interests evolve. This could help models prioritize content or actions that support longer-term user goals, like learning or deep exploration.

**Combining Vision with Behavioral Data**

Integrating computer vision techniques with behavioral signals (e.g., clicks, scrolling, typing) provides a multimodal approach that enhances the accuracy of user engagement measurements. Visual cues such as gaze tracking, facial expressions, and body language can offer additional insights into a user's level of interest or emotional response to content.

### Final Thoughts

As models increasingly evaluate human behavior, the traditional roles of evaluator and evaluated are reversing. Developing algorithms that can infer users' reward functions will play a crucial role in maintaining engagement while guiding users toward their long-term objectives. 

For instance, should a robot arm deliver a fourth Krispy Kreme doughnut to a user just because they ask for it? While it satisfies immediate desires, it may not align with the user's long-term health goals. (Apologies to Krispy Kreme—I am a big fan of your work.)

![[krispy.jpg|200]]`


Clearly, advancing IRL presents exciting opportunities for enhancing user engagement and satisfaction, it also presents challenges that must be addressed. Developing more efficient methods for converting user actions into meaningful data to steer models will unlock valuable new capabilities. These models can provide guidance and evaluate user preferences as they shift and fluctuate over time.

By incorporating advanced engagement metrics—including time spent, re-engagement frequency, query depth, and visual cues—models can better understand and anticipate user needs. However, integrating modalities like computer vision necessitates careful consideration of privacy and ethical implications to ensure that user data is protected and that models promote well-being without compromising individual autonomy.

As we continue to develop models with new capabilities for integrating information about users across data streams, it's imperative that we ensure these systems enhance human experience without sacrificing progress towards users and organization's long-term interests. 
