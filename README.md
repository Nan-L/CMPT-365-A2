# CMPT-365-Blind Helper

credit by: Nan Liu, Joshil Patel

This program is to help bilind people who are not hearing-impaired to constract a picture of what a sense of vison could convey by sense of hearing.

Firstly, it is known that each ear can process only about 15kB/s of information, so we’ll have to reduce the resolution of each video frame, and temporally subsample our video down to only one image per second or even less.

This program use a small image of size only 64 × 64 pixels. To obtain this image from each video frame, create a luminance image via the (very rough) NTSC guide:  Y′ = 0.299 ∗ R′ + 0.587 ∗ G′ + 0.114 ∗ B′
where R′, G′, B′ are gamma-corrected (i.e., ordinary) camera signals. We’ll simply use this grey image Y′, and abandon colour.

The program subsample the image down to 64 × 64 pixels.

Since the ear is limited in loudness and frequency, let’s also reduce the intensity resolution of the uploaded image frame down to just 4 bits, making an image with only 16 levels. The program’ll tie the image intensity to the sound loudness that generated before.

The program trying to make a sound picture, and a simple way to do this is to associate up the y-axis with higher frequencies, and down with lower ones. Each column of our image has 64 pixels. So for the top pixel, use the highest frequency; the bottom pixel will have the lowest frequency.

To make a sound picture, proceed across the image by columns, 64 columns per second. For each column, produce a “chord” of sound, with each frequency sounded tied to the pixel position, and the loudness given by the pixel intensity. Note that this means that if 30 pixels of the column are black, say, then those 30 frequencies will not be present in the chord sounded.

At the end of every frame, sound an audible “click”, to signal a new image starting.

An interesting extra feature would be to have the sound pan from left to right as the progress across the image, assuming the program have two stereo audio channels.
