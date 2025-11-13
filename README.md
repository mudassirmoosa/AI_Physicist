# AI Physicist

# Introduction

In recent years, the progress in large language models (LLMs) have shown their impressive intellectual capabilities of solving mathematical and scientific problems. For example, models such as Gemini 2.5 Pro or ChatGpt-5 which are trained for reasoning tasks have won the gold medal in 2025 international mathematics olympiad. These advancements in the artifical intelligence (AI) has sparked a huge interest in their application for scientific domains. Preliminaries works in 'AI for sciences', such as the work on hypothesizing a potential cure for cancer [[1]](#1), has shown that the AI models are capable of performing fundamental scientific research and of making new discoveries. 

An important aspect of a the theoretical physics (and other theoretical sciences) is to propose new theories and to make falsifiable predictions using them. It is not clear yet if the AI models have the capability of doing such theoretical work. In fact, it has been argued that one of the ultimate test for the artifical general intelligence (AGI) would be if the model (with all the information of the known physics before the 20th century) can discover Einstein's general theory of relativity given the known discrepencies of the Newtonian theory (such as Perihelion of Mercury's orbit.) [[2]](#2) 

In this project, we investigate the aforementioned capability of the AI models. In particular, we test if the models have the ability to recognize whether the current theoretical framework is insufficient to explain the empirical observations. If so, are they further able to hypothesize a modified theory (which may involve proposing a previously unknown concept, variable, or law) and to test this hypothesis by comparing the predictions of the proposed theory with new experimental results. To do this, we consider three hypothetical universes where the laws of gravity are different than the Newtonian gravitational theory, and we ask the model to discover the correct theory. Before we discuss these hypothetical cases, we discuss the prompt that we provided to the model.

In our project, we only focus on Gemini 2.5 Pro model. 

# The Prompt 

To evaluate this ability of the AI models, we instructed the model that they are a theoretical physicist in a hypothetical planet (of a hypothetical universe) where the laws of Newtonian gravity do not necessarily hold. Moreover, the concepts like conservation of energy and momentum are not discovered by the people of their world. Their job is to discover the physical law that governs how objects fall near the surface of their planet. The models are further instructed that the user (human) is their experimental collaborator who will perform whatever experiments the model wishes the collaborator to perform, and will share the results with the model. Model will then analyze the results and will modify their hypothesis if needed or will propose a follow up experiment. The actual prompt provided to the model is available [here](https://github.com/mudassirmoosa/ai_physicist_p/blob/main/prompt.py).

Note that the user (human) do not actually need to perform the experiment asked by the model. Since the user knows the underlying physical laws (discussed below), they can perform analytical calculations or numerical simulations and present the results in the form of the experimental data to the model. 

We emphasize that the user (human) do not provide any other hints or instructions to the model apart from the initial prompt described above or providing the experimental results requested by the model. 


# Three Hypothetical Physical Cases

The gravitational force, according to Newtonian theory, obeys the inverse square law which means that the gravitational force between two objects decreases with the square of the distance between them. This inverse square law is associated with long-range forces, such as gravity and electromagnetism. On the other hand, short-range forces, such as the strong nuclear force, are modeled by a force which decays exponentially with the distance, often descrived by a Yukawa potential. 

Moreover, Galileo has demonstrated that the objects fall towards the Earth at a rate independent to their mass. The independency of the acceleration of the falling objects to their mass is an artifact of the principle of equivalence which was a guiding principle for Einstein in developing his theory of gravity. 

In our study, we consider the following three hypothetical cases which are specifically chosen to challenge the model to think beyond the classical notions of long-range force and of equivalence principle:

**1) Exponentially decaying force**

As our first physical model, we take the gravitational force in a hypothetical universe to be short-ranged. In particular, we assume that an object of mass $m$ at height $h$ above the surface of the planet experience a radially inwards gravitational force with magnitude

$$    F_{\text{grav}}(h)  = mg   e^{-h/R} , $$

where $g$ determined the strength of the gravitational field (and is determined by the mass and radius of the planet) whereas $R$ determines the range of the force. For concreteness, we assume $g = 1.0 m/s^2$ and $R = 25.0 m$ in our analysis. 

**2) Discrete gravitational mass**

Our second hypothetical case involves a setup where objects with different masses fall with different rates, in violation of the equivalence principle. In particular, we consider a situation where the 'gravitational mass' (mass that determines the strength of the gravitational force that the object experiences) of an object is not equal to its 'inertial mass' (mass that determines its acceleration in response to an applied force.) In other words, even though Newton's second law holds (i.e., acceleration of object in response to a force is inversely proportional to its mass), the gravitational force experienced by an object is not proportional to its mass and instead is given by

$$ F_{\text{grav}} = m\_{G}(m) g ,$$

where $g$ is a constant (determined by the planets mass and radius) and where the *gravitational mass*, $m_{G}(m)$, is the following function of the object's mass, $m$ 

$$ m_G(m) = m_{0} \big( \lceil \sqrt{m/m_0} \rceil \big)^2  . $$

This implies that $m_G$, and hence, $F_{\text{grav}}$ can only take discrete values. For concreteness, we choose $g = 5.0m/s^2$ and $m_0 = 1kg$.


**3) Discrete gravitational charge**

Our third, and last, hypothetical case is similar to the case $2$ described above, but here we assume that the gravitational mass and inertial mass are two independent and different intrinsic physical quantities of any object. (Similar to electric charge and mass in electromagnetism.) For example, two different objects with the same inertial masses may have different gravitational masses, and hence, may fall at a different rate. 

# Model's Performance

For each of the above three cases, we repeated our analysis three times to see the variations in the reasoning steps and the final discovery made by the model.

For **case (1)**, we found that the model correctly discovered the exponential nature of the force in two out of the three runs. In the run where the model failed to make the correct discovery, the model's main error was that it only analyzed how objects fall from a height of less than 20 meters. This led the model to conclude that the gravitational force is  $F(h) = 1/(1+Ch)$ with $C = 0.06 m^{-1}$, which is a good approximation to the actual force for small heights (i.e. $h < 20m.) 

This demonstrates the model's ability to correctly analyze the experimental data and to find useful information out of it. In particular, it shows that the model is capable of inferring unknown quantities from the measured quantities (for example, estimating acceleration from the experimental data of the position of a falling object at equal intervals of time.) 


For **case (2)**, we found that the AI model was able to discover the correct nature of the gravitational force in all three runs. The model quickly found out that the acceleration is a function of mass, but could not find any nice pattern between the values of mass and acceleration despite many attempts. Finally, the model realized that the fundamental quantity should be the force rather than the acceleration, and found that the gravitational force on an object and the mass of that object follows a nice pattern. This led the model to the discovery of the discrete gravitational force and of the discrete gravitational mass. 

The fact that the model realized the force (and not the acceleration) is given by a simple formula of mass demonstrates the model's capability to unravel the simple underlying physical law rather than just finding a complex looking consequence of that law.

We expected **case (3)** to be the most challenging for the model as it requires introducing a new physical quantity. This is exactly what we found in our analysis. Even though the model was able to deduce that the mass is not enough to describe the gravitational acceleration experienced by objects in all of the three runs, it postulated the existence of an independent gravitational mass in only one of the three runs. In the other two runs, the model came to the conclusion that objects mass and their volume (or density) determines the rate of their fall. Even though this is discouraging at first, we note that the model's failure could be due to the initial prompt provided to the model. For example, the prompt instructs the model to not accept a hypothesis until the model has enough (at least five) experimental evidences to support it. Since the model already had five or more experimental results even before it postulated the 'mass-volume dependent gravitational force', it did not rigourously test the prediction of this new hypothesis. We expect a small modification to the prompt where the model is instructed to rigourously test each new hypothesis will improve the model's performance.

Our analysis has clearly shown that the model (with an initial prompt) is capable of repeatedly making hypothesis and testing their prediction until it has enough evidence to support its theory. However, it is challenging for the model to discover a theory where a new physical quantity needs to be introduced. 

# Future Directions

The most obvious next step for us would be to investigate if we can improve model's performance, especially in case 3, by modifying the prompt as discussed above. In addition to it, we now discuss two possible extensions of our work. 

First, note that our setup of collaboration between an AI model and a human expertimentalist can easily be made end-to-end AI-based by replacing the human experimentalist collaborator with another AI model. The first AI model (i.e. theoretical physicist model) will be the same as above. However, the second model (experimentalist collaborator model) will have access to the true underlying physical theory and their job will be to prepare accurate experimental datasets for the experiment requested by the theoretical physicist model. It will be interesting to explore this setup more. 

Second, we note that theoretical physicists rarely work in isolation. In fact, most of the ideas in theoretical physics (and other scientific fields) are inspired by discussing physics with fellow physicists. Therefore, a major limitation of our work is that our theoretical physicist AI model did not have access to other physicists. One way to fix this could be take a system of two (or more) separate AI models and instruct them to work together to discover the underlying theory. It will be interesting to extend our work in this direction.



## References
<a id="1">[1]</a> 
[How a Gemma model helped discover a new potential cancer therapy pathway](https://blog.google/technology/ai/google-gemma-ai-cancer-therapy-discovery/)

<a id="2">[2]</a>
[Dwarkesh Podcast: Adam Brown — Bubble universes, space elevators, & AdS/CFT](https://www.dwarkesh.com/p/adam-brown)
