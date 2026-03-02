# Chinese Discovery Dish Alternative
A little bit cheaper, portable dish antenna for general weather satellite reception.

![](pictures/L-band_winter.jpg)

## Getting the dish
Search "LTE MIMO Dish antenna" or "LTE Dish antenna" on AliExpress and you are likely to find it in the top results. You can also try negotiating with seller to buy the dish alone (for a lower price of course) without the mount and the feed, as you'll need different feed for weather satellite reception anyway. The price seems to fluctuate a lot and it's worth waiting for a sale or discount.

## Dimensions
The four reflector plates are made out of powder coated aluminum, fit in a regular backpack and assemble into a 60cm prime focus dish.

![](pictures/backpack.jpg)

Standard metric hardware is supplied with the dish. M5 for assembling the plates, M6 for attaching the feed/feedarm adapter. I ended up using the supplied bolts, but replaced the nuts with stainless wing nuts to simplify the assembly. Four M6 and eight M5 wing nuts are needed. For attaching the backfire helix, i used three M4x16 nylon bolts with nylon nuts. 

## The feed and feedarm
Like i said earlier, you won't be needing the original feed. It's very wideband, linearly polarized... and doesn't perform the best even on linear signals. I highly recommend Digitelektro's backfire helix:
https://github.com/Digitelektro/BackfireHelix  
For the feedarm, i'm using a 20 mm aluminum pipe with two printed adapters (provided in "3d models" directory). I also recommend cutting a notch in the pipe, to prevent damage to the coax when the dish is dropped.

![](pictures/feedarm_coax_notch.jpg)

The backfire helix side adapter is aweeri's ***backfire_helix_compact_adapter_for_discovery_dish.STL***, i just added slots for M4 nuts and removed one bolt hole.  
Unfortunately the backfire helix requires tuning the S11 return loss/SWR to perform well, and it's not very beginner friendly because of it. VNA and some tuning knowledge are required. Here is how i do it, but do keep in mind, there are another ways!

![](pictures/matching_1.jpg)
![](pictures/matching_2.jpg)

When tuning using a simple matching strip, two rough rules are worth acknowledging:  
**distance between the matching strip and feedpoint affects the center frequency**,  
**distance between the matching strip and director affects the S11 Return Loss/SWR**.  

#### The elephant in the room (connecting LNAs to the feed)
As you can see, i opted to connect the LNA to the feed with a short coax. To make it easier, i used a female SMA on the feed. This of course sacrifises a little bit of SNR, as we are adding insertion loss between feed and LNA, and possibly some noise trough coax shield as well. However, i think it's more convinient than having the LNA build into the feedarm, and also ensures the LNA enclosure does not affect the radiation pattern.

## Dish assembly
I recommend assembling the dish on a flat, level surface. Start with connecting all plates together with bolts, but without tightening them. Put the dish reflector-side down on a flat surface, and now gradually tighten the bolts. Then attach coax to your feed, mount the feedarm and the helix itself.

## Focal point adjustments
To get the best performance, i recommend adjusting the focal point on a test signal, like Elektro L2/L3/L4 for L-band, or SBIRS-GEO 1 (USA 230) for S-band.
SatDump software is commonly used for weather satellite reception, and it has the required pipelines (at least for L-band) to live decode the signal for real time SNR feedback.
For L-Band just use Elektro-L and the GGAK pipeline, then adjust the focal lenght while watching the SNR. Keep in mind that GGAK pipeline is notoriously "fiddly" to get a lock, sometimes you'll have to tick the SDR frequency a couple kHz up or down to get a lock. If you don't have Elektro-L LOS, Arktika M2 also transmits GGAK on 1703 MHz, and there's a pipeline for it as well, named accordingly. Keep in mind Arktika M1 does not transmit GGAK at all, and M2 does it only at certain altitudes, usually > 30000 km.
For S-band it's a bit trickier. You'll have to use advanced mode, and make temporary changes to Metop AHRPT pipeline (modulation to oqpsk, symbol rate to 2500000):

![](pictures/usa_230_sband_test.jpg)

Then assemble your S-Band setup, set the frequency to 2262.5 MHz and point your dish at SBIRS-GEO 1 (USA 230). Once you get a SNR readout, you can start adjusting the focal point for best SNR.

## Performance on popular weather satellites
I've decided to included some performance numbers on weather satellites i commonly receive with this setup.

### Meteor M2-x

![](pictures/Low_el_Meteor_HRPT.jpg)
![](pictures/Meteor_HRPT.jpg)

### Metop B/C
Keep in mind Metop B has intermittent modulator issues, that cause distorted constellation and lower SNR.
![](pictures/Metop_C.jpg)
![](pictures/Metop_B_broken_constellation.jpg)

### Elektro L2

![](pictures/Elektro_L2_GGAK.jpg)

### Arktika M2 

![](pictures/Arktika_M2_GGAK.jpg)

### Proba 2

![](pictures/Proba_2.jpg)

### DMSP F17

![](pictures/DMSP_F-17.jpg)

