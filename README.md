# Predictive Hydrogen Leak Detection and Localization (Machine Learning)

Inside this digital folder sits output from a study done at NLR's (National Laboratory of the Rockies) ESIF lab. Hydrogen leaks indoors were tracked by combining sensors with smart algorithms. The goal was to spot where gas escapes occur. Tools learned patterns from collected signals. Location guesses came after analysis of those readings. Work centered on making detection faster and more accurate. 

Floating unseen, hydrogen slips by without smell or shade, yet packs risk where air sits still. This work pulls numbers from linked sensors to track its presence so that it can: 
- detect a leak quickly,
- start by guessing the spot where water first escaped,
- ensure better spots for sensors help labs react more quickly. Placement matters when speed is key. Quick detection starts with where devices sits. Labs gain time through a smarter setup. Response improves when tools are positioned well. 

## What the project does
Using data over time from 16 stationary hydrogen detectors, the system estimates where a leak happens. That spot shows up as an X and Z point. 

Two modeling approaches are included:
1. **Artificial Neural Network (ANN)**  
   - From signal data, it spots trends that point to where leaks happen. The system uses past readings to guess problem spots before they grow. 
   - One approach used training with a single loss type, another mixed in a second option during testing. Each method shaped results       differently, depending on the data flow through the model layers the usual measure of average squared differences. 
   - A different kind of error measure focuses more on big mistakes, giving them higher importance because being far off matters most. This approach adjusts how much each mistake affects the result, especially when accuracy is critical. 

2. **K-Nearest Neighbors with Dynamic Time Warping (K-DTW)**  
   - Looking at old data helps spot patterns that match today's readings. What stands out is how closely some earlier results resemble the current one. Matching now means checking what happened before. Sometimes it is clear right away when comparisons fit well. The closest examples come from times with nearly identifcal conditions. 
   - Signals might shift their pace, like when heating systems alter schedules, but time warping adjusts them anyway. Matching stays accurate because the method bends timelines slightly. Timing mismatches fade once alignment kicks in behind the scenes. 
   - The spot where a leak might be is found by taking the middle point of the nearest similar cases. 

## Data summary
- From various tests and computer models, different ways in which leaks happen were studied. 
- A span of 2,000 seconds fills every situation with data from sensors. That stretch of time carries measurements without pause. Every moment within it adds to the full picture captured.
- Sensors keep recording throughout each case presented.
- Training a model targets the initial 1,000 seconds. That stretch shapes how it learns patterns early on. Time matters most right at the beginning. What happens after that comes later. Focus stays locked on those opening moments. 
- Temperature readings might lag behind actual changes. This happens because heating systems alter airflow patterns. Sensors could react too late. Air currents push warm or cool pockets around. Reading drift without warning. Equipment behavior affects timing. Delays appear even if sensors work perfectly. 

> Note: When the original dataset isn't part of this repository, supplying your own formatted files become necessary, like CSVs tracking sensor readings across time, along with labeled leak locations. Instead of waiting, prepare those inputs ahead of time. What matters most? Matching the structure exactly. Otherwise, mismatches creep in without warning. Files must line up, step by step. One wrong column order breaks everything later. Labels, especially those coordinates, can't be missing or shifted. So double-check each file before moving forward. 

## Results (example comparison)
During testing, the neural network using penalty-sensitive loss made fewer mistakes in pinpointing leaks compared to the version without that feature and also outperformed the K-DTW method. The numbers show how far off each prediction was from the actual leak spot, measured in meters.


## How to run (typical workflow)
1. **Prepare data**
   - A single moment holds 16 streams of sensor readings, tagged by when they happened. Each chunk comes with exact coordinates showing where the link began, both X and Z positions marked clearly. Time passes inside every file, recorded across those 16 paths. Location isn't guessed, but rather it sits there in numbers alongisde the flow of measurements. Every case wraps timing, signals, and spots into one package. 

2. **Preprocess**
   - Fix gaps in data, merge situations when required, then adjust input sizes accordingly.

3. **Train**
   - Start by setting up the artificial neural network training process. Following that, proceed with executing the K-DTW assessment phase. One step leads into the next without overlap. Each method operates on its own track yet feeds into the larger goal. Processing continues until both tasks complete their cycles. 

4. **Evaluate**
   - Looking at where leaks were expected versus where they actually happened helps measure accuracy. The gap between these points shows how far off predictions were. Distance in meters tells the size of each mistake. Results get added up to show overall performance. This summary gives a clear picture of reliability. 

## Tools often used
- Python
- pandas / NumPy
- scikit-learn (preprocessing + tuning)
- TensorFlow and Keras for ANN training.

## Future improvements
- Throw in extra spots where leaks happen, along with bigger gaps and higher pressure levels.
- Experimenting helps adjust K-DTW using extra samples. Sometimes tweaking works better when fed larger sets.
- Feeding it richer inputs often sharpen results.
- More instances refine how it aligns sequences.
- Start by checking performance in alternate labs, since air movement varies there. Sensors might react differently because of how space shapes flow patterns. 

## Acknowledgements
Work finished under a DOE Office of Science internship, backed by NLR, guided closely by Munjal Shah. 

## Safety note
Working on this helps explore ideas through trial. Real protection setups need physical safeguards instead of just software. Warning signals must make sense when they go off, not confuse people. Always check how things work when machines are actually running.




