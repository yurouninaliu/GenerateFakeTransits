# GenerateFakeTransits

This project aims to generate fake transits through machine learning. This can be used to augment training data for transit detection algorithms. Compared to deterministic transit generation algorithms, which generally assume perfect conditions, machine learning algorithms can generate realistic noise and asymmetries. It can also be faster at generating transits after training.
I tried to use both a Variational Autoencoder (VAE) and a Conditional Variational Autoencoder  (cVAE) to train on TESS observed transiting exoplanets. 
For the VAE, the TESSdata.ipynb notebook queries transit data from TESS and saves the data in a pkl (Pickle) file. It saves all confirmed transiting exoplanets that have been observed by TESS for 120 second exposures. If a target has multiple valid sectors, the code treats them as individual transits. The code also phase folds each transit. Together, the file contains 4949 transits.
Then you can run VAE.ipynb with the downloaded file. The Python environment I used to run VAE.ipynb is in requirements.txt. As shown in Figure 1 and 2, the VAE model generates curves with dips in them, but the dips are sharp instead of U-shaped like transits.
   
Figure 1. Reconstructed transit using VAE, zoomed in on right panel
 
Figure 2. Fake Transits Generated with VAE model
The CVAE model improves on this by conditioning on transit depth, transit duration, and transit impact parameter. In particular, including the transit duration may help the model learn that transits should have flatter dips. The data used for CVAE can be downloaded with TESSdata_conditional.ipynb. Note that because I only download transits where transit depth, transit duration, and transit impact parameter are all know, there are significantly less transits available for training, at only 448 transits.
The CVAE model is trained in cVAE.ipynb and loaded in loadcVAE.ipynb. Note that the model shown in the output of cVAE.ipynb is not the one saved and loaded in loadcVAE.ipynb. The saved and loaded model is the one I’ll use for generating graphics. As shown in Figure 3, compared to the reconstructed curve of VAE (Figure 1), the reconstructed curve of CVAE is much better. It emulated the U-shape of the original curve significantly better. However, because the number of transits decreased for the CVAE model, we can see from Figure 4 that there are significant fluctuations in generated fake transits compared to Figure 2.
 
Figure 3. Reconstructed transit using CVAE
 
Figure 4. Fake Transits Generated with CVAE model
Next, we want to explore how well the CVAE model responds to changes in conditions that it was trained on. Figure 5 shows how the reconstructed transit responds to changes in transit depth, duration, and impact parameter. The model conditions of transit depth quite well. Clearly the depth of transit increases as the depth parameter increases. However, the model responds to changes to the duration parameter non-physically. It does increase the transit duration but also alters the shape of the transit to be less U-shaped. The model does not respond to changes in impact parameter well. The shape of transit remains essentially unchanged with changing impact parameter.
   
Figure 5. Reconstructed transits with changes in conditions
It is understandable that the CVAE does not behave perfectly, as it is trained on a dataset of size 448. Future directions may include discarding impact parameter as a condition to increase the number of valid transits, or including transits from other telescopes to increase the dataset size.
