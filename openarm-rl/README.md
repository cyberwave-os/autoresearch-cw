# OpenArm pick and place RL

Objective of this task: Train a RL model that moves a OpenArm with 2 wrist cameras and a RealSense on top and accomplishes 70% success rate on pick and place of a paper cup, from one area of a table to the other. 

To accomplish this, you have:

* Access to the Cyberwave MCP with a valid token (dev environment). With this, you can add RL tasks and run simulations and much more
* Access to a Cyberwave environment that fits our use case https://app-dev.cyberwave.com/vittorio-banfis-workspace-3/envs/autolearner-openarm
* Access to the Cyberwave remote labs. You will find a remote lab that mirrors the setup described above
* Full access to this MacBook Pro (I installed XCode and Homebrew)

Proceed as follows:

1. Read the Cyberwave documentation to learn how to write RL models in a way that follows the Cyberwave guidelines
2. Using the Cyberwave MCP, download the Mujoco zip file of the environment above
3. Write and train a RL task to accomplish the goal
4. Upload it to Cyberwave, run a simulation and observe the video result. Decide if you accomplished the goal or if you need to go back to (3)
5. Once you are satisfied, access the remote lab feature of Cyberwave, release the RL model there, run the RL model as controller of the real open arm device
6. Check the video of the real device and decide if you accomplished the goal or you need to go back to (3)

Do not stop or ask for user feedback until you are done.