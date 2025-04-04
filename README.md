# GenerateFakeTransits

This project aims to generate fake transits through machine learning. This can be used to augment training data for transit detection algorithms. Compared to deterministic transit generation algorithms, which generally assume perfect conditions, machine learning algorithms can generate realistic noise and asymmetries. It can also be faster at generating transits after training.

I use a Variational Autoencoder (VAE) to train on TESS observed transiting exoplanets. The TESSdata.ipynb notebook queries data from TESS and saves the data in a pkl (Pickle) file. Running the notebook will at least take several hours, so I encourage you to download the file I compiled from here[https://drive.google.com/file/d/1g8SyFSnE9F_xQ34sJX7RezE4uFxutExn/view?usp=sharing]. Then you can run VAE.ipynb with the downloaded file. The Python environment I used to run VAE.ipynb is in requirements.txt.

To Malena and Konsti: Definitely don't run TESSdata.ipynb, as it will take forever. The dependencies of VAE.ipynb are a bit strange and may be hard to set up. I think it's not worth it to run it.
