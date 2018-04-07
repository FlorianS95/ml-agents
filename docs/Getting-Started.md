If you havn't done the installation and setup, do the installation [here](Installation.md)

## Play an example environment using pretrained model

1. In the Project window, go to `Assets` -> `ML-Agents` -> `Examples` -> `3DBall` folder and open the `3DBall` scene file. 
2. In the Hierarchy window, click on `Ball3DAcademy` -> `Ball3DBrain`. 
3. In the Inspector window, under `Brain (Script)` -> `Brain Type`, change the `Brain Type` to `Internal`. 
4. Click the `Play` button and you will see the platforms automatically adjusts itself using the pretrained model.

If you want to train your own model:

## Training your own model in the example environment

### Building the Environment

The first step is to open the Unity scene containing the 3D Balance Ball
environment:

1. Launch Unity.
2. On the Projects dialog, choose the **Open** option at the top of the window.
3. Using the file dialog that opens, locate the `unity-environment` folder 
within the ML-Agents project and click **Open**.
4. In the `Project` window, navigate to the folder 
`Assets/ML-Agents/Examples/3DBall/`.
5. Double-click the `Scene` file to load the scene containing the Balance 
Ball environment.

![3DBall Scene](images/mlagents-Open3DBall.png)

Since we are going to build this environment to conduct training, we need to 
set the brain used by the agents to **External**. This allows the agents to 
communicate with the external training process when making their decisions.

1. In the **Scene** window, click the triangle icon next to the Ball3DAcademy 
object.
2. Select its child object `Ball3DBrain`.
3. In the Inspector window, set **Brain Type** to `External`.

![Set Brain to External](images/mlagents-SetExternalBrain.png)

Next, we want the set up scene to to play correctly when the training process 
launches our environment executable. This means:
* The environment application runs in the background
* No dialogs require interaction
* The correct scene loads automatically
 
1. Open Player Settings (menu: **Edit** > **Project Settings** > **Player**).
2. Under **Resolution and Presentation**:
    - Ensure that **Run in Background** is Checked.
    - Ensure that **Display Resolution Dialog** is set to Disabled.
3. Open the Build Settings window (menu:**File** > **Build Settings**).
4. Choose your target platform.
    - (optional) Select “Development Build” to
    [log debug messages](https://docs.unity3d.com/Manual/LogFiles.html).
5. If any scenes are shown in the **Scenes in Build** list, make sure that 
the 3DBall Scene is the only one checked. (If the list is empty, than only the 
current scene is included in the build).
6. Click *Build*:
    a. In the File dialog, navigate to the `python` folder in your ML-Agents 
    directory.
    b. Assign a file name and click **Save**.

![Build Window](images/mlagents-BuildWindow.png)

### Training the Brain with Reinforcement Learning

Now that we have a Unity executable containing the simulation environment, we 
can perform the training. To first ensure that your environment and the Python 
API work as expected, you can use the `python/Basics` 
[Jupyter notebook](Background-Jupyter.md). 
This notebook contains a simple walkthrough of the functionality of the API. 
Within `Basics`, be sure to set `env_name` to the name of the environment file 
you built earlier.

### Training with PPO

To summarize, go to your command line, enter the `ml-agents` directory and type: 

```python
python3 python/learn.py <env_file_path> --run-id=<run-identifier> --train 
```
**Note**: If you're using Anaconda, don't forget to activate the ml-agents environment first.

The `--train` flag tells ML-Agents to run in training mode. `env_file_path` should be the path to the Unity executable that was just created. 

### Observing Training Progress

Once you start training using `learn.py` in the way described in the previous section, the `ml-agents` folder will 
contain a `summaries` directory. In order to observe the training process 
in more detail, you can use TensorBoard. From the command line run:

`tensorboard --logdir=summaries`

Then navigate to `localhost:6006`.

From TensorBoard, you will see the summary statistics:

### Embedding the trained model into Unity

1. The trained model is stored in `models/<run-identifier>` in the `ml-agents` folder. Once the 
training is complete, there will be a `<env_name>.bytes` file in that location where `<env_name>` is the name 
of the executable used during training. 
 2. Move `<env_name>.bytes` from `python/models/ppo/` into 
`unity-environment/Assets/ML-Agents/Examples/3DBall/TFModels/`.
3. Open the Unity Editor, and select the `3DBall` scene as described above.
4. Select the `Ball3DBrain` object from the Scene hierarchy.
5. Change the `Type of Brain` to `Internal`.
6. Drag the `<env_name>.bytes` file from the Project window of the Editor
to the `Graph Model` placeholder in the `3DBallBrain` inspector window.
7. Press the Play button at the top of the editor.

If you followed these steps correctly, you should now see the trained model 
being used to control the behavior of the balance ball within the Editor 
itself. From here you can re-build the Unity binary, and run it standalone 
with your agent's new learned behavior built right in.