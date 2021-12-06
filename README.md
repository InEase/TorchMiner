![GitHub Repo stars](https://img.shields.io/github/stars/InEase/TorchMiner) ![PyPI](https://img.shields.io/pypi/v/torchminer)
# Description

TorchMiner is designed to automatic process the training, evaluating and testing process for PyTorch DeepLearning, with a simple API.

You can access all Functions of TorchMiner simply use `Miner`.

## Quick Start

```python
import TorchMiner
from TorchMiner import Miner
from TorchMiner.plugins.Logger.Jupyter import JupyterLogger, JupyterTqdm
from TorchMiner.plugins.Metrics import MultiClassesClassificationMetric
from TorchMiner.plugins.Recorder import TensorboardDrawer

miner = Miner(
    alchemistic_directory='/the/route/to/log', 
    train_dataloader=train_dataloader, 
    val_dataloader=val_dataloader,  

    model=model, 
    loss_func=MSELoss,  
    optimizer=optimizer,  
    experiment="the-name-of-experiment",  # Subdistribution in the experimental directory
    resume=True,  # Whether to automatically load the previous model
    eval_epoch=1,  # How many rounds are evaluated
    persist_epoch=2,  # How many rounds are saved once a checkpoint
    accumulated_iter=1,  # How many times iterates the parameter update after accumulation
    in_notebook=True,
    amp=True,  # Whether to use amp
    plugins=[
        # Use the plugins to extend the function of miner
        JupyterLogger(),
        JupyterTqdm(),
        # The two above plugins are designed to get better output in Jupyter Enviroment
        MultiClassesClassificationMetric(),
        # This Plugin can automaticly calculate Accuracy, kappa score and Confusion Matrix in Classification problems.
        TensorboardDrawer(input_to_model),
        # This Plugin can record the informations generate by training process or by other plugins in Tensorboard.
    ],
)

# And then, trigger the training process by
miner.train()
