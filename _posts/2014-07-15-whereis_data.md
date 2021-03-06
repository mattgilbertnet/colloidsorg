---
title: Why is it taking so long to post data? Data organization
date: 2014-07-15 00:15:30 Z
categories:
- operations
- science
layout: post
image: images/homepage/square186.png
---

# Data organization cannot be defined before the experiment runs

We have received hundreds of images from the first three runs, and the current fourth run, from ACE-M2 over the past few weeks. Yet I haven't been posting very much in the way of analysis. Why? It's not because I haven't received or looked at the image, but because of another fundamental challenge: how the data is organized and presented to us (as the PIs) from NASA and ZIN, who are running the experiment.

### We don't know ahead of time what data we will take

NASA typically has an engineering culture, where goals are specified, often with mind-numbing specificity, and criteria for progress and success defined. This is fine when the task to be accomplished can actually be defined ahead of time, as in the design, engineering, fabrication, launch and operation of a piece of equipment. But this mentality is a less convenient fit for scientific experiments, where the main objective is to learn something _newe_ about a scientific phenomenon. This is especially true in our little corner of soft-matter physics, where we do experiments quickly, change things rapidly in response to what we see, then do another experiment---much like the "fail quickly" mentality of Silicon Valley startups. 

### Lots and lots of potential data we could collect

To that end, we launched a wide range of samples of different kinds of materials: dyes, suspensions of colloids in solvent, and colloid-polymer mixtures that undergo phase separation and gelation. The LMM microscope has several objective lenses (2.5x, 10x, 20x, 40x, 63x, 100x) and several modes of imaging (bright-field, fluorescence) and the fluorescence mode has several filters to excite and detect at different wavelengths. And within each sample, there are several different locations that we could image, and a variety of depths. So there are thousands upon thousands of possible choices we can make to collect an image from the sample.

This tremendous flexibility makes ACE a potentially powerful experiment, but at the cost of simplicity. With BCAT, we had a single view (fill the frame with the sample), and only one sample at a time---which takes several weeks to run. The data involves a single time series of a few hundred images, which get nicely zipped up and posted weekly by our extremely talented and hardworking point-woman at ZIN, Cathy Frey. Nonetheless, while the BCAT data is now easy to organize, it took several years and probably a dozen runs before we got our stride in what images to collect. With ACE, the problem is probably two orders of magnitude more complex!

### Existing data structure therefore represents a best-guess by engineers years in advance

At the moment, there is a relatively byzantine file-folder structure that places images from data sets in a tree labeled by a number of things, including date, experiment number, and objective lens. We didn't know what samples we were going to launch until a few months before delivery, because we need always to keep the experiments as up-to-date as possible, to make sure we are using the most advanced sample preparation and to tie into the science that is actually interesting *now*. As convenient as it is for the bureacrats, specifying these things years in advance only guarantees that the results are not interesting to anyone.

By contrast, the instruments (e.g. the LMM) must undergo years of development and testing before launch, and simply cannot wait until we have samples ready, because of all of the constraints in engineering that operating on-board the ISS requires. So the engineers who build the hardware and design the software and protocols *cannot possibly know* what the actual experiments will be. This is the challenge of the long-latency structure of operating experiments in microgravity (and is absolutely not endemic to NASA; ESA has exactly the same issues, as do other agencies).

All of this is **absolutely not a criticism** of anyone or any part of the process. It's just a big challenge that we must overcome to be successful in doing real, dynamic, new science onboard the ISS. Nevertheless, this leads to an important truth:

## The organization, transmission, storage and curation of data is a fundamental part of doing both proper engineering and actual new science onboard the ISS, which is almost never mentioned, and people never really think about.

It's basically assumed that, by some magical process, whatever data the PI wants will magically appear online, which they should hurry up and download, analyze, and get results back *this week* to send results back to everyone in the weekly science summary.

For any given week, I can tell you what the science summary is: we got data, and we are trying to figure out what we are looking at, and if it's correct. Jumping to any more rapid conclusions---or, worse yet, trying to spread the message in public, to the press, or via social media---is courting cold-fusion disaster. Yes, the news cycles are quick, and people want an instant reaction or result spread immediately. 

*Unfortunately, the process of actually doing science is limited by human brainpower, and all evidence suggests that social media makes us if anything stupider. I certainly haven't become faster at fundamental understanding due to the advent of social media, though others may be more talented.*

Nonetheless, the process of understanding what is happening quickly improves with experience. We had a good idea what we were seeing by the third round of BCAT phase-separation samples (though recent data from BCAT-KP is fundamentally different---therefore quite exciting---but then we are back to not know what is going on---and that's where the fun is). But ACE is a complex experiment where everything is new, and the main reason we launched so many different kinds of samples is that we didn't know what to expect!

And this is where the data organization is a big challenge, basically of the chicken-and-egg type. We don't know what images we are going to collect, so we can't specify how it should be organized. So we get what the engineers thought would work best, basically what is logical from a collection standpoint, which almost by definition is not going to be ideal for the science. So it is an enormous task to sort everything out, and validate the data: how do I know that an image I open up on my computer is from the right sample, with the combination of parameters (lenses, camera settings, position, depth, etc.)? 

Ultimately, there needs to be a *combined, close effort between the science-based PIs and engineers (in concert with operations)* to define the right procedures for collecting, labeling, and transmiting the right data from ISS to NASA on the ground and ultimately to us in the lab who will analyze the data. To do this, we need first to understand the challenges of the existing systems, as well as the scientific requirements, then develop a proposal for moving forward. **And this cannot be done before actually acquiring and receiving significant data from ISS; there is no way to do this ahead of time!** 

# Limitations of the current data organization

The current way data is collected and stored on LMM has several fundamental issues which must be resolved before the set of images collected onboard ISS becomes usable experimental data. Just as the raw voltage levels from each pixel of the camera need to be assembled into a digital image, those images must be assembled into well-organized, well-documented collections in order to be at all useful. And those images must be connected

### Metadata is not stored with the images

The *metadata* of each image, including the camera settings (exposure, gain, black-level offset), microscope settings (objective lens, filter, illumination), sample location (sample well, and x-y-z position within it) are not stored in the image itself, for example in metadata fields within a TIF image (which could easily defined to contain this). The software that writes the image to disk does not incorporate any of this information with the image itself. So there is no "self-documentation" of each image, which represents a good practice in general, especially when we have so many images. Anything else quickly becomes prone to error.

### Some information is stored in the directory

Right now, which sample well and platter, which can be [mapped 1-to-1]({% post_url 2014-03-06-ace_m2_sample_layout %}), then the objective, and the depth within the sample, are each stored in various directories / folders, within which the images for each day are sorted. There are additional levels of folders for the timing (seconds elapsed since experiment was run) and an experiment number defined by the operator.

### When a number is assigned to an experiment, and what an experiment includes, varies significantly

As we are defining what data to collect, what amount corresponds to a new experiment number has varied both over time, and between operators. So data gets put into new experiments in some places in a way that is not the same as other, ostensibly identical data. 

### File names are basically all the same

This is a significant problem when it comes to data organization. A typical filename is ```00001_00000.tif```, and in fact remains the same for different samples, and different days. Thus, if a file is moved out of its directory, all information is lost and it cannot be checked to see where it came from.

Moreover, when we look at the evolution of samples over time, having the same exact filename means I cannot simply drag images from the same place, objective, depth, and settings from successive days into the folder, but have to rename each one individually, without direct access by the operator who collected the images. This makes any form of automated analysis impossible, and even manual analysis is a challenge to even keep track of what images I am looking it.

Of course, there was no obvious way to specify how the engineers could have added the right information ahead of time, not knowing what samples would be, how we would look at them, etc. etc. Probably the best they could have done was to generate a random alphanumeric code as part of each image's filename, which could then be later correlated, but that would not have been much of an improvement.

*Instead, what we need is a comprehensive plan to organize the data we have collected, which involves close cooperation between us on the science / PI side, the engineers who designed the hardware and wrote the software, and the operators who actually collect the data.* So here's the current proposal for how to move forward, which I and Louis Chestney (who wrote the software and collected a lot of great data) came up with:

# How we plan to organize things

Unfortunately, there is no perfect, or even optimal way, to organize the data, involving thousands of images from dozens of samples on dozens of days of operations. We have a number of constraints, conceptual and practical, that have to be addressed.

There is always a tension between organizing the data in a way that is best for the subsequent analysis, and one that reflects the history of how it was collected. The problem is that the history can be haphazard, in our case jumping around to take different samples at different settings. And the analysis is never defined until basically it's done, and we don't want to have to do this process more than once.

Moreover, there is a limit to the number of characters that fit comfortably within a filename before some of the computer systems that handle the files get unhappy (thank you IBM and Microsoft from the 1980s for this horrid legacy).

So for the most common / redundant parts of the metadata, such as well, sample number, and objective, we use folders to hold that information. This is more for convenience and making it easy to check / validate the images, as well as consult historical records. For things that change each run that are important (e.g. sample position, date), we put that in the filename, which also serves to document . And for the less-important things (camera settings), we keep that information in a separate database of sorts.

## Folder organization

The first set of folder hierarchies correspond to what sample well we are looking at, since that is the way the raw data is actually collected (i.e. at one well at a time). So the first three levels of directory structure [with examples] are :

### 1. Platter [```platter_2105```]

We have two platters (2104, 2105) in ACE-M2, and one platter with our samples (2109) in ACE-M3.

### 2. Strip [```strip_E_618```]

Each platter has three strips, so A-C (with their numbers) are contained in sample 2104, D-F are in 2105, and G is in 2109.

### 3. Well [```well_E4_s22```]

Each strip has five wells, numbered 1-5, and each well contains a sample (1-22 in ACE-M2, and probably 23-27 in ACE-M3). 

With these levels, the directory for each well identifies its platter, strip and sample, all by number, which can be double-checked against the documentation, and gives a very quick reminder exactly what sample is being looked at. There may be path length limitations, in which case we might have to shorten these names.

Now, within this, there are two fundamental ways we could organize the data:

+ by date, creating a new folder each day, and within that, subfolders for the different magnifications and positions.

+ by objective lens, so that data from each magnification is stored closely, and then within that organize by date.

There are several advantages and disadvantages to each approach. Because we are looking at the evolution of samples over time, and we want to compare images collected under nearly-identical conditions over time, it makes most sense to group by all other parameters besides time first, and then have the images in the smallest subfolders differ only in time they were collected. This also facilitates the analysis, because the same operation applied to each image within a folder makes sense only when the images represent the same conditions and positions.

Therefore, within each well folder, we have several more levels of subfolder:

### 4. Objective lens / magnification [```10x```]

We image each sample with several objective lenses, and each sample has a different combination used. We have ultimately standardized the [data collection operations]({% post_url 2014-07-01-ace_m2_ops %}) to take 2.5x survey images, tile the full sample at 10x, and zoom into selected areas and collect tiled images at 20x and 40x magnification. The 2.5x images do not focus on a specific depth, so those images will sit in the 2p5x folder. Everything else must be more carefully specified, by how deep into the sample the images were collected.

### 5. Depth into the sample from the coverslip [```z060um```]

These will be the main folders that hold the data of interest. In particular, there should only be a single image from a single day (with the exception of near-identical duplication for redundancy). For the 2.5x, the image is of the whole sample chamber. For the 10x, there is a single composite of the entire well. For the 20x and 40x images, there are composites of smaller areas. Individual images that form the source of each composite can then be held in a subfolder, once for each day. 

### 6. Date of data collection [```179```]

Everything NASA does uses the 3-digit numeric day of the year, which is convenient because it's short, sequential, and takes up on three characters.

Because the composites will be properly labeled, as long as the folder of the source images can be identified, these images need not have unique names (preferred but not necessary), since they will always be referenced to the uniquely-named composite images.

Therefore, the example path for the folder would be:

```
/platter_2105/strip_E_618/well_E4_s22/10x/z060um/
```

## Naming files

The next step is to define a file naming convention. We want to preserve as much information to identify uniquely the image in a transparent way, especially when it gets moved to a different folder (e.g. for analysis). To that end, the sample platter, strip, well, and sample should be included, in the most compact form minimizing characters but preserving the unique parts of the information (since the more complete info can be read from the directories).

+ ```p4``` for platter 2104, ```p5``` for platter 2105, etc.
+ ```a``` for strip A, ```b``` for strip B, etc.
+ ```1``` for well 1 on that strip, ```2``` for well 2 on that strip, etc.
+ ```s01``` for sample 1, ```s02``` for sample 2, etc.; two digits cover all samples
+ ```02x``` for 2.5x magnification, ```10x``` for 10x magnification, etc.; two digit numbers
+ ```z060``` for 60 micron depth relative to cover slip, ```z100``` for 100 micron depth, etc.; three digit numbers
+ ```xy1``` for first composite xy-position, ```xy2``` for second, etc; ```xyA``` for position A of individual image within a composite, ```xyB``` for position B, defined by the maps/tables. Composites are distinguished by the number, where individual images have a letter. No composite has more than 16 unique positions, so a single character is sufficient.
+ ```180``` for 180th day of the year, etc. for other dates
+ ```15520``` for experiment number 15520, to tie back into the log books.

So a complete filename and path in the example would be:

```
/platter_2105/strip_E_618/well_E4_s22/10x/z060um/p5e4s22_10x_z060_xy1_180_15520.tif
```

This preserves a lot of information for each sample, and correlates it back to the date it was collected and the experiment number, which contains all of the imaging and position parameters. This way, if any image gets separated from its directory structure, all of the information can be reconstructed and recovered.

# Practical implementation

Ultimately, we will have to set up a data store for both we as the scientific team, and ZIN as the engineers and operators, to have common access to move around and rename files appropriately. As you can imagine, this will take a significant amount of time and effort all around. This is an absolutely critical task that needs to be done before any data can be analyzed carefully. There may be some basic results which I present, but this organization is required before any full, systematic analysis can take place. And that is what we will be working on a lot going forward.
