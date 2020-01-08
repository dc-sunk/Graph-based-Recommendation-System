# Graph-based-Recommendation-System
## Structure of our repository
	.
	|-- README.md (here)
	|-- log (saved tensorboard log file)
	|-- ml-100k (dataset)
	|-- parameters (weights)
	|-- text (grid search text and ablation study results)
	|-- dataset.py
	|-- train.py
	|-- model.py
	|-- utils.py
	|-- loss.py

## Guideline to run our code:
### STEP 1: install required packages
```bash
pip: pip install -r requirements.txt   
conda: conda env create -f environment. yaml
```

### STEP 2: run code
```bash
python3 train.py --rate_num 5 \
                --lr 0.01 \
                --weight_decay 0.00001 \
                --num_epochs 1000 \
                --hidden_dim 5 \
                --side_hidden_dim 5 \
                --out_dim 5 \
                --drop_out 0.0 \
                --split_ratio 0.8 \
                --save_steps 100 \
                --log_dir './log' \
                --saved_model_folder './weights' \
                --dataset_path './ml-100k' \
                --save_processed_data_path './processed_dataset' \
                --use_side_feature 1 \
                --use_data_whitening 1 \
                --use_laplacian_loss 1 \
                --laplacian_loss_weight 0.05
```
You can observe the loss curve through the training by runing:
```bash
tensorboard --logdir=log/name_of_your_saved_file
```
<p align="center">
  <img width="700" height="300" src="image/loss_curve.png"/>
</p>
<p align="center">Figure 1: Loss curve.
</p>

## Gridsearch for best hyperparameters by running shell script:
```console
sh run.sh -lr 0.01 0.02 -epochs 1000 2000 -hidden_dim 3 5 -side_hidden_dim 3 5 -dropout 0 0.1 0.2 -use_side_feature 0 1 -use_data_whitening 0 1 -use_laplacian_loss 0 1 -laplacian_loss_weight 0.05 0.1 | tee -a text/gridsearch.txt
```
The reult(RMSE) will be saved in a **gridsearch.txt** under the text folder.
