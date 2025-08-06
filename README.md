## SuperPrepare
This is an affiliated repo of SuperHugeAAD. MATLAB preprocessing codes and examples provided.

# Included datasets
* Anhui University (AHU)'s (ID=1)
* DTU's (ID=2)
* Estart (ID=3)
* Alice's storys (not used later, so no dataset ID is given).
* KUL's 2016 (ID=4)
* KUL's 2023 (eye-gaze control, ID=5)
* National University of Singapore's (ID=7)
* Peking University's (4 talker, 4 directions, ID=8)
* KUL's sparKULee (AAD challenge in ICASSP 2023 and 2024, single taker, ID=9)
* And ours: Nanjing University's (2 talker, 15 directions, ID=6)

# Prepare your own dataset
There are several scripts you need to change

1. `.\utils\load_data_struct.m` If your dataset is like sparKULee (put EEG trials in separate `.npy` files), do like the `sparKULee` case: skip this function, and load your trial later. If your data is in `csv` or other table-like format, do as in the `AHU` case. Otherwise, we expect the `dataset_path` refers to a `.mat` file which can be passed to `load()` and returns a structure (no matter how the data stored inside the structure).
2. `.\utils\get_dataset_info.m`: Follow existing implementations to fill in each variables in your own case. If some field is inaccessible, leave it to empty `[]`.
3. `.\utils\extract_trials.m`: In this function, you need to write your codes to implement extracting an EEG trial from the dataset structure, along with its corresponding audio and labels (if possible). Follow our existing implementations and find examples there.
4. `.\config.mlx`: Add your dataset to the end of `all_datasets` variable, such that a unique dataset ID is given. Change `raw_dataset_names` and `preprocessed_dataset_names` accordingly. If you do not wish to process other datasets, change `raw_dataset_names = ["name_of_your_dataset"]` (if you have raw files) and/or `preprocessed_dataset_names = ["name_of_your_dataset"]`.
5. [OPTIONAL] `.\utils\load_stimuli.m`: If your dataset contains audio waveform, envelopes and others, you can load them here.
6. TAKE CARE: MATLAB treats single quote `'` and double quote `"` differently. We recommend using double quote (string array) instead of single quote (cell array of characters). If you write `['a','b','c']`, all you get is a single scalar `'abc'`.
7. Check other settings as you wish.
