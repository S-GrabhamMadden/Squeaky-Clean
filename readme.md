# Squeaky Clean
#### _For USV Audio Noise Scrubbing_

As part of a larger project to do with USV analysis, I put together a few algorithms for noise reduction to run as a pre-processing step before other analysis. After some interest was expressed in using this step separately, I've separated it out.

##### Note:

- This is designed for 50kHz-range "affective" type USV calls of rats.
- The default parameters were tuned to the specific USV files my project worked with, some tweaking might be necessary to best fit your data.

## Use

**Running the Script**
The noise reduction is done through a python script. With your USV audio files (in WAV format) in a directory, run the script with the following command:
```sh
python SqueakyCleanUSVs.py dir/to/use
```
This will create a subdirectory with cleaned versions of each audio file separately. Feel free to examine the results and tweak parameters if necessary.

By default, the bandpass filter starts to attenuate out below 34kHz and above 68kHz as this performed best for our files. You can change these values arbitrarily by running the script like this (in this example the filter attenuates below 25kHz and above 70kHz):
```sh
python SqueakyCleanUSVs.py dir/to/use --bandpassLow 25000 --bandpassHigh 70000
```

## Explanation
For now, the script is fairly simple. It just runs a combination of a band-pass filter and spectral gating with a noise threshold. This is good for some kinds of noise like background hum, but weak against loud irregular noise like bumps. For now, I'd recommend looking through your audio in a tool of your choice (I use audacity) after running the script, to crop out obvious noise the script missed - it will be very visually distinct from actual USVs.

This isn't a full solution to noise in USV processing, but hopefully using this to preprocess data might speed up the process of tackling noise with other tools. In the future, this tool could be extended to be "smarter" by identifying bumps through spikes in amplitude across a broad frequency spectrum, as opposed to the whistle shapes of USVs.
