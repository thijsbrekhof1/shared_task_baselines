#Documentation for running the baseline systems – Group 04
Step 1: running the models themselves:
#Task A monolingual:
python3 baseline_task_A.py --train_file_path subtaskA_train_monolingual.jsonl --test_file_path subtaskA_dev_monolingual.jsonl --prediction_file_path subtaskA_distilbert_predictions_monolingual.jsonl --subtask A --model 'distilbert-base-uncased'
#Task A multilingual:
python3 baseline_task_A.py --train_file_path subtaskA_train_multilingual.jsonl --test_file_path subtaskA_dev_multilingual.jsonl --prediction_file_path subtaskA_distilbert_predictions_multilingual.jsonl --subtask A --model 'distilbert-base-multilingual-cased'
#Task B:
python3 subtaskB/baseline/transformer_baseline.py --train_file_path subtaskB_train.jsonl --test_file_path subtaskB_dev.jsonl --prediction_file_path subtaskB_distilbert_predictions_monolingual.jsonl --subtask B --model 'distilbert-base-uncased'
#Task C:
-
This results in a predictions file as specified under the ‘--prediction_file_path’ argument. This prediction file can then be evaluated using scorer.py. This python file also uses format_checker.py so make sure you also have that file installed in the same directory. 
#Task A monolingual:
python3 subtaskA/scorer/scorer.py --gold_file_path=subtaskA_dev_monolingual.jsonl --pred_file_path=subtaskA_distilbert_predictions_monolingual.jsonl
#Task A multilingual
python3 subtaskA/scorer/scorer.py --gold_file_path=subtaskA_dev_multilingual.jsonl --pred_file_path=subtaskA_distilbert_predictions_multilingual.jsonl
#Task B: 
python3 subtaskB/scorer/scorer.py --gold_file_path=subtaskB_dev.jsonl --pred_file_path=subtaskB_distilbert_predictions_monolingual.jsonl
#Task C:
-
