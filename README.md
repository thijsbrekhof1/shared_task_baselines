# Documentation for running the baseline systems – Group 04

## Step 1: running the models themselves:

Run the scripts for each model by downloading the data files from https://github.com/mbzuai-nlp/SemEval2024-task8#data_format and running the models as shown below.

Important is to set two environment variables, exp_name and seed_value.
exp_name is to set a different name to test/model you are running to compare later.
seed_value is to set a static seed_value to re-create random scenarios.

### Task A monolingual:

python3 baseline_task_A.py --train_file_path subtaskA_train_monolingual.jsonl --test_file_path subtaskA_dev_monolingual.jsonl --prediction_file_path subtaskA_distilbert_predictions_monolingual.jsonl --subtask A --model 'distilbert-base-uncased'

### Task A multilingual:

python3 baseline_task_A.py --train_file_path subtaskA_train_multilingual.jsonl --test_file_path subtaskA_dev_multilingual.jsonl --prediction_file_path subtaskA_distilbert_predictions_multilingual.jsonl --subtask A --model 'distilbert-base-multilingual-cased'

### Task B:

python3 subtaskB/baseline/transformer_baseline.py --train_file_path subtaskB_train.jsonl --test_file_path subtaskB_dev.jsonl --prediction_file_path subtaskB_distilbert_predictions_monolingual.jsonl --subtask B --model 'distilbert-base-uncased'

### Task C:

python transformer_baseline.py --model_path "severinsimmler/xlm-roberta-longformer-base-16384" --train_file "../data/subtaskC_train.jsonl" --load_best_model_at_end True --dev_file "../data/subtaskC_dev.jsonl" --test_files ../data/subtaskC_dev.jsonl --metric_for_best_model "eval_mean_absolute_diff" --greater_is_better False --do_train True --do_predict True --seed $seed_value   --output_dir "./runs/$exp_name" --logging_dir "./runs/$exp_name/logs" --num_train_epochs 10 --per_device_train_batch_size 32 --per_device_eval_batch_size 32 --auto_find_batch_size True --logging_steps 10 --load_best_model_at_end True --evaluation_strategy "epoch" --save_strategy "epoch" --save_total_limit 2

This results in a predictions file as specified under the ‘--prediction_file_path’ argument. This prediction file can then be evaluated using scorer.py. This python file also uses format_checker.py so make sure you also have that file installed in the same directory.

### Task A monolingual:

python3 subtaskA/scorer/scorer.py --gold_file_path=subtaskA_dev_monolingual.jsonl --pred_file_path=subtaskA_distilbert_predictions_monolingual.jsonl

#### Task A multilingual

python3 subtaskA/scorer/scorer.py --gold_file_path=subtaskA_dev_multilingual.jsonl --pred_file_path=subtaskA_distilbert_predictions_multilingual.jsonl

### Task B:

python3 subtaskB/scorer/scorer.py --gold_file_path=subtaskB_dev.jsonl --pred_file_path=subtaskB_distilbert_predictions_monolingual.jsonl

### Task C:

python ./scorer.py --pred_file_path ./runs/exp_1/predictions/subtaskC_dev.jsonl --gold_file_path ../data/subtaskC_dev.jsonl
