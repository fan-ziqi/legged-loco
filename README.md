# Legged Loco
This repo is used to train low-level locomotion policy of Unitree Go2 and H1 in Isaac Lab.

<p align="center">
<img src="./src/go2_teaser.gif" alt="First Demo" width="45%">
&emsp;
<img src="./src/h1_teaser.gif" alt="Second Demo" width="45%">
</p>


## Installation
1. Create a new conda environment with python 3.10.
    ```shell
    conda create -n isaaclab python=3.10
    conda activate isaaclab
    ```

2. Make sure that Isaac Sim is installed on your machine. Otherwise follow [this guideline](https://docs.omniverse.nvidia.com/isaacsim/latest/installation/install_workstation.html) to install it. On Ubuntu 22.04 or higher, you could install it via pip:
    ```shell
    pip install isaacsim-rl==4.1.0 isaacsim-replicator==4.1.0 isaacsim-extscache-physics==4.1.0 isaacsim-extscache-kit-sdk==4.1.0 isaacsim-extscache-kit==4.1.0 isaacsim-app==4.1.0 --extra-index-url https://pypi.nvidia.com
    ```

3. Install PyTorch.
    ```shell
    pip install torch==2.2.2 --index-url https://download.pytorch.org/whl/cu121
    ```

4. Clone the Isaac Lab repository, and link extensions.
    ```shell
    git clone git@github.com:isaac-sim/IsaacLab.git
    cd IsaacLab
    cd source/extensions
    ln -s {THIS_REPO_DIR}/isaaclab_exts/omni.isaac.leggedloco .
    cd ../..
    ```

5. Run the Isaac Lab installer script and additionally install rsl rl in this repo.
    ```shell
    ./isaaclab.sh -i
    ./isaaclab.sh -p -m pip install -e {THIS_REPO_DIR}/rsl_rl_leggedloco
    cd ..
    ```


## Usage
* train

    ```shell
    python scripts/train.py --task=go2_base --history_len=9 --run_name=XXX --max_iterations=2000 --save_interval=200 --headless

    python scripts/train.py --task=h1_base --run_name=XXX --max_iterations=2000 --save_interval=200 --headless
    ```

* test

    ```shell
    python scripts/play.py --task=go2_base_play --history_len=9 --load_run=RUN_NAME --num_envs=10
    python scripts/play.py --task=h1_base_play --load_run=RUN_NAME --num_envs=10
    ```

    Use `--headless` to enable headless mode. Add `--enable_cameras --video` for headless rendering and video saving.

## Add New Environments
You can add additional environments by placing them in the `isaaclab_exts/omni.isaac.leggedloco/omni/isaac/leggedloco/config` directory