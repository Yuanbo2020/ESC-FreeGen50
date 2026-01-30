# ESC-FreeGen50

[Paper Code](https://github.com/Yuanbo2020/U-ART) 

The dataset described herein is based on the publicly available ESC-50 benchmark dataset, augmented with self-collected samples and samples synthesized through generative audio models.

## Data Composition

[ESC-50](https://github.com/karolpiczak/ESC-50) is a widely used benchmark dataset for environmental sound classification. It contains 2,000 labeled environmental audio recordings (each 5 seconds long, covering 50 semantic categories) and is suitable for the comparative evaluation of environmental sound classification methods.

Building upon the ESC-50 category system, the extended dataset constructed in this project retains the original 50 semantic definitions while expanding the sample size to 100 audio clips per category. The specific composition is as follows:

- **40 clips** derived from the original ESC-50 segments.
- **10 clips** manually selected from public field recordings such as Freesound.org.
- **50 clips** synthesized using AudioLDM2.

![dataset_pie](assets/dataset_pie.jpg)

This composition adheres to the original specifications and has been verified through manual listening to ensure the sound features align with the semantic labels. To reduce label noise and interference from multiple events, each audio clip in the dataset is constrained to contain **one single salient audio event**. We utilized manual screening to strictly enforce this constraint.

## Data Sources

1. **ESC-50 Original Samples (40 clips/class)**
   - Original recording segments consistent with the category labels were directly adopted from ESC-50, retaining their original sampling rate and duration information (standard ESC-50 clips are 5 seconds). These samples serve as a real-world environmental sound baseline, providing a solid supervision signal for the model.
2. **Public Field Recordings (10 clips/class)**
   - Recordings matching the target category semantics were retrieved from open audio resources such as Freesound.org. These were manually screened and cropped to ensure **single-event dominance** (i.e., each segment contains only one primary audio event). The cropping process also ensured that the duration of the obtained clips matches that of the ESC-50 dataset. Basic cleaning (deduplication, noise level screening) and manual auditing were performed on these samples to guarantee semantic consistency and audio quality.
3. **Synthetic Samples (50 clips/class, using AudioLDM2)**
   - Using AudioLDM2 (based on pre-trained weights), audio clips of the corresponding duration were generated using the category labels as text prompts. The generated results underwent item-by-item manual listening to filter out samples with mismatched semantics or poor audio quality, retaining only those that met quality requirements. The pre-trained weights and model implementation used are available at the official AudioLDM repository (https://huggingface.co/cvssp/audioldm2). This synthesis process aims to expand the data diversity of each category.

## Data Split

To support model training, hyperparameter tuning, and fair evaluation, the dataset is divided according to the following ratios and sample sizes (Total sample size: 100 clips/class across 50 classes):

- **Training Set**: Total of 4,000 samples (50 classes × 80 clips/class). These samples are used for model parameter learning. The training set contains a mixture of the three sources mentioned above to ensure the model benefits from both the robustness of real recordings and the diversity brought by synthetic samples.
- **Validation Set**: Total of 500 samples (50 classes × 10 clips/class). Used for hyperparameter tuning and early stopping determination.
- **Test Set**: Total of 500 samples (50 classes × 10 clips/class). Used for final performance evaluation. The samples in the test set are independent of the training/validation sets in terms of semantics and specific sources to minimize evaluation bias.

## Mel-Spectrogram Comparison (Label vs. LLM Prompt)

We provide mel-spectrogram comparisons for all 50 classes under `assets/mel_spectrograms`. Each image contrasts:

- **Direct label prompt** into AudioLDM2.
- **LLM-generated prompt** (from the same label) into AudioLDM2.

Across the 50 categories, the LLM-generated prompts yield cleaner harmonic structures, more stable temporal patterns, and stronger label-consistent energy distributions in the spectrograms, indicating better overall generation quality compared with direct label prompts.

Below are the 50 comparison figures:

![airplane](assets/mel_spectrograms/airplane_mel_comparison.png)
![breathing](assets/mel_spectrograms/breathing_mel_comparison.png)
![brushing_teeth](assets/mel_spectrograms/brushing_teeth_mel_comparison.png)
![can_opening](assets/mel_spectrograms/can_opening_mel_comparison.png)
![car_horn](assets/mel_spectrograms/car_horn_mel_comparison.png)
![cat](assets/mel_spectrograms/cat_mel_comparison.png)
![chainsaw](assets/mel_spectrograms/chainsaw_mel_comparison.png)
![chirping_birds](assets/mel_spectrograms/chirping_birds_mel_comparison.png)
![church_bells](assets/mel_spectrograms/church_bells_mel_comparison.png)
![clapping](assets/mel_spectrograms/clapping_mel_comparison.png)
![clock_alarm](assets/mel_spectrograms/clock_alarm_mel_comparison.png)
![clock_tick](assets/mel_spectrograms/clock_tick_mel_comparison.png)
![coughing](assets/mel_spectrograms/coughing_mel_comparison.png)
![cow](assets/mel_spectrograms/cow_mel_comparison.png)
![crackling_fire](assets/mel_spectrograms/crackling_fire_mel_comparison.png)
![crickets](assets/mel_spectrograms/crickets_mel_comparison.png)
![crow](assets/mel_spectrograms/crow_mel_comparison.png)
![crying_baby](assets/mel_spectrograms/crying_baby_mel_comparison.png)
![dog](assets/mel_spectrograms/dog_mel_comparison.png)
![door_wood_creaks](assets/mel_spectrograms/door_wood_creaks_mel_comparison.png)
![door_wood_knock](assets/mel_spectrograms/door_wood_knock_mel_comparison.png)
![drinking_sipping](assets/mel_spectrograms/drinking_sipping_mel_comparison.png)
![engine](assets/mel_spectrograms/engine_mel_comparison.png)
![fireworks](assets/mel_spectrograms/fireworks_mel_comparison.png)
![footsteps](assets/mel_spectrograms/footsteps_mel_comparison.png)
![frog](assets/mel_spectrograms/frog_mel_comparison.png)
![glass_breaking](assets/mel_spectrograms/glass_breaking_mel_comparison.png)
![hand_saw](assets/mel_spectrograms/hand_saw_mel_comparison.png)
![helicopter](assets/mel_spectrograms/helicopter_mel_comparison.png)
![hen](assets/mel_spectrograms/hen_mel_comparison.png)
![insects](assets/mel_spectrograms/insects_mel_comparison.png)
![keyboard_typing](assets/mel_spectrograms/keyboard_typing_mel_comparison.png)
![laughing](assets/mel_spectrograms/laughing_mel_comparison.png)
![mouse_click](assets/mel_spectrograms/mouse_click_mel_comparison.png)
![pig](assets/mel_spectrograms/pig_mel_comparison.png)
![pouring_water](assets/mel_spectrograms/pouring_water_mel_comparison.png)
![rain](assets/mel_spectrograms/rain_mel_comparison.png)
![rooster](assets/mel_spectrograms/rooster_mel_comparison.png)
![sea_waves](assets/mel_spectrograms/sea_waves_mel_comparison.png)
![sheep](assets/mel_spectrograms/sheep_mel_comparison.png)
![siren](assets/mel_spectrograms/siren_mel_comparison.png)
![sneezing](assets/mel_spectrograms/sneezing_mel_comparison.png)
![snoring](assets/mel_spectrograms/snoring_mel_comparison.png)
![thunderstorm](assets/mel_spectrograms/thunderstorm_mel_comparison.png)
![toilet_flush](assets/mel_spectrograms/toilet_flush_mel_comparison.png)
![train](assets/mel_spectrograms/train_mel_comparison.png)
![vacuum_cleaner](assets/mel_spectrograms/vacuum_cleaner_mel_comparison.png)
![washing_machine](assets/mel_spectrograms/washing_machine_mel_comparison.png)
![water_drops](assets/mel_spectrograms/water_drops_mel_comparison.png)
![wind](assets/mel_spectrograms/wind_mel_comparison.png)
