# `hattorijaponic`

## Data generation

```shell
python neighbors/data/create_neighborhood.py --output_dir /tmp/tmp --max_rand_len 10 --language_group hattorijaponic --lang all --pairwise_algo lingpy --random_target_algo markov --logtostderr --task_data_dir ~/projects/ST2022/data  --num_duplicates 100
```

## Training

```shell
python neighbors/model/trainer.py  --run_locally=cpu --model=feature_neighborhood_model_config.TransformerWithNeighborsTiny --input_symbols /tmp/tmp/hattorijaponic.syms --output_symbols /tmp/tmp/hattorijaponic.syms --feature_neighborhood_train_path tfrecord:/tmp/tmp/hattorijaponic_train.tfrecords --feature_neighborhood_dev_path tfrecord:/tmp/tmp/hattorijaponic_test.tfrecords --feature_neighborhood_test_path tfrecord:/tmp/tmp/hattorijaponic_test.tfrecords --learning_rate=0.001 --max_neighbors=9 --max_pronunciation_len=13 --max_spelling_len=10 --logdir /tmp/logdir/
```

## Inference

```shell
python neighbors/model/decoder.py --feature_neighborhood_test_path=tfrecord:/tmp/tmp/hattorijaponic_test.tfrecords --input_symbols /tmp/tmp/hattorijaponic.syms --output_symbols /tmp/tmp/hattorijaponic.syms --ckpt /tmp/logdir/train --model=TransformerWithNeighborsTiny --decode_dir /tmp/tmp/decode_dir/ --split_output_on_space --max_neighbors=9 --max_pronunciation_len=13 --max_spelling_len=10 --batch_size 1
```

Latest model from `/tmp/logdir/train/ckpt-00019005`.