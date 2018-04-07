# Installation & Set-up

To install and use ML-Agents, you need install Unity, clone this repository
and install Python with additional dependencies. Each of the subsections
below overviews each step, in addition to an experimental Docker set-up.

## Install **Unity 2017.1** or Later

[Download](https://store.unity.com/download) and install Unity. If you would
like to use our Docker set-up (introduced later), make sure to select the 
_Linux Build Support_ component when installing Unity.

<p align="center">
    <img src="images/unity_linux_build_support.png" 
        alt="Linux Build Support" 
        width="500" border="10" />
</p>

## Clone the ml-agents Repository

Once installed, you will want to clone the ML-Agents GitHub repository. 

    git clone git@github.com:Unity-Technologies/ml-agents.git

The `unity-environment` directory in this repository contains the Unity Assets
to add to your projects. The `python` directory contains the training code.
Both directories are located at the root of the repository. 

## Install Python (with Dependencies)

In order to use ML-Agents, you need Python 3 along with
the dependencies listed in the [requirements file](../python/requirements.txt).
Some of the primary dependencies include:
- [TensorFlow](Background-TensorFlow.md) 
- [Jupyter](Background-Jupyter.md) 

### Windows Users

If you are a Windows user who is new to Python and TensorFlow, follow [this guide](Installation-Windows.md) to set up your Python environment.

### Mac and Unix Users

If your Python environment doesn't include `pip`, see these 
[instructions](https://packaging.python.org/guides/installing-using-linux-tools/#installing-pip-setuptools-wheel-with-linux-package-managers)
on installing it.

To install dependencies, go into the `python` subdirectory of the repository,
and run from the command line:

    pip3 install .

## Setting up ML-Agent within Unity

1. Open Unity and use it to open folder `ml-agents`/`unity-environment`. 
2. Go to `Edit` -> `Project Settings` -> `Player`
3. For each of the platforms you target 
(**`PC, Mac and Linux Standalone`**, **`iOS`** or **`Android`**):
    1. Go into `Other Settings`.
    2. Select `Scripting Runtime Version` to 
    `Experimental (.NET 4.6 Equivalent)`
    3. In `Scripting Defined Symbols`, add the flag `ENABLE_TENSORFLOW`. 
    After typing in, press Enter.
4. Go to `File` -> `Save Project`
5. Restart the Unity Editor.

## Setting up TensorflowSharp Support

[Download](https://s3.amazonaws.com/unity-ml-agents/0.3/TFSharpPlugin.unitypackage) TensorflowSharp plugin, and import it into Unity once downloaded by double clicking on it.  You can see if it was successfully imported by checking the TensorFlow files in the Project window under `Assets` -> `ML-Agents` -> `Plugins` -> `Computer`. 

**Note**: If you don't see anything under `Assets`, drag the `ml-agents`/`unity-environment`/`Assets`/`ML-Agents` folder under `Assets` within Project window.

## Docker-based Installation (Experimental)

If you'd like to use Docker for ML-Agents, please follow 
[this guide](Using-Docker.md). 

## Help

If you run into any problems installing ML-Agents, 
[submit an issue](https://github.com/Unity-Technologies/ml-agents/issues) and
make sure to cite relevant information on OS, Python version, and exact error 
message (whenever possible). 


