Learning to Simulate Dynamic Environments with GameGAN
Seung Wook Kim, Yuhao Zhou, Jonah Philion, Antonio Torralba, Sanja Fidler
CVPR, 2020
[Paper] [Project Page] [Video]

Abstract: Simulation is a crucial component of any robotic system. In order to simulate correctly, we need to write complex rules of the environment: how dynamic agents behave, and how the actions of each of the agents affect the behavior of others. In this paper, we aim to learn a simulator by simply watching an agent interact with an environment. We focus on graphics games as a proxy of the real environment. We introduce GameGAN, a generative model that learns to visually imitate a desired game by ingesting screenplay and keyboard actions during training. Given a key pressed by the agent, GameGAN "renders" the next screen using a carefully designed generative adversarial network. Our approach offers key advantages over existing work: we design a memory module that builds an internal map of the environment, allowing for the agent to return to previously visited locations with high visual consistency. In addition, GameGAN is able to disentangle static and dynamic components within an image making the behavior of the model more interpretable, and relevant for downstream tasks that require explicit reasoning over dynamic elements. This enables many interesting applications such as swapping different components of the game to build new games that do not exist.

For business inquiries, please visit our website and submit the form: NVIDIA Research Licensing

Citation
If you found this codebase useful in your research, please cite:
@inproceedings{kim2020learning,
  title={Learning to Simulate Dynamic Environments with GameGAN},
  author={Kim, Seung Wook and Zhou, Yuhao and Philion, Jonah and Torralba, Antonio and Fidler, Sanja},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={1231--1240},
  year={2020}
}
Environment Setup
This codebase is tested with Ubuntu 18.04 and python3.8.3

Clone the repository
git clone https://github.com/nv-tlabs/GameGAN_code.git
cd GameGAN_code
Install dependencies
pip install -r requirements.txt
Dataset extraction
Please clone and follow https://github.com/hardmaru/WorldModelsExperiments/tree/master/doomrnn to install the VizDoom environment.

Copy extraction scripts and run
cp data/extract.py DOOMRNN_DIR/
cp data/extract_data.sh DOOMRNN_DIR/
cd DOOMRNN_DIR
./extract_data.sh
Now, extracted data is saved in 'DOOMRNN_DIR/vizdoom_skip3'
cd GameGAN_code/data
python dataloader.py DOOMRNN_DIR/vizdoom_skip3 vizdoom
You should now see .npy files extracted in 'data/vizdoom' directory.
For custom datasets, you can construct .npy files that contain a sequence of image and action pairs and define a dataloader similar to 'class vizdoom_dataset'. Please refer to 'data/dataloder.py'.

-- The above repository is deprecated and VizDoom environment might not run correctly in certain systems. In that case, you can use the docker installtaion of https://github.com/zacwellmer/WorldModels and copy the extraction scripts in the docker environment.

Training
We provide training scripts in './scripts'.

For training the full GameGAN model, run:
./scripts/vizdoom_multi.sh
For training the GameGAN model without the external memory module, run:
./scripts/vizdoom_single.sh
Monitoring
You can monitor the training process with tensorboard:
tensorboard --port=PORT --logdir=./results
Tips
Different environments might need different hyper-parameters. The most important hyper-parameter is 'recon_loss_multiplier' in 'config.py', which usually works well with 0.001 ~ 0.05.
Environments that do not need long-term consistency usually works better without the external memory module
About
Learning to Simulate Dynamic Environments with GameGAN (CVPR 2020)

Resources
 Readme
License
 View license
 Activity
 Custom properties
Stars
 238 stars
Watchers
 10 watching
Forks
 41 forks
Report repository
Releases
No releases published
Packages
No packages published
Contributors
2
@seung-kim
seung-kim
@daniel-kukiela
daniel-kukiela Daniel Kukieła
Languages
Python
99.3%
  ######
This emulates nvidia gamegan and can use urls anything to game
#######
EMUGAN
#
