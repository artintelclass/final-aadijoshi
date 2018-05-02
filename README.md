# Final

## Download
The model can be downloaded from [here](https://drive.google.com/open?id=1Qkc6AV_go3XApkRrCN5VGR4NjXMYt1QH)

## Introduction
The goal of this project was to create a tool that could assist comic book creators visualize what a rough sketch would look like once it was improved and generated on the computer. This would be extremely useful during the brainstorming phase, for example. Instead of having to produce a detailed sketch, or having to use a graphics editor, the author could create a rough sketch and then get an idea of what the final product would look like.

## Process
Attempt 1: Style transfer
The first idea I had was to use style transfer. The sketch that is provided as input could be seen as the 'edges' of a photo after edge detection. For example, the sketch of a city skyline and a photo of a city skyline, after it passes through an edge-detection algorithm, would be similar. Given an input image, then, the goal would be to find a similar image in the database, apply style transfer to the image, and output the new image. Furthermore, the input image could be broken down into smaller 'layers' that would be decided by the user. If an image consists of a house and car, rather than looking for similar images in the database, an output image could be created by applying style transfer to a house and a car seperately, then layering them together.

The advantage of this method was that it could turn a two-dimensional sketch into a more realistic 'three-dimensional' one. For example, a building could be drawn as a rectangle on paper. After the image passes through the program, a photo of a real building would be outputted, although style transfer would be applied to this photo.

After testing out style transfer on a photo, however, I decided to drop this idea. The result of applying a 'comic' style transfer to a city skyline can be seen here: ![result](https://drive.google.com/open?id=18bUdAK_2APMa_usko24DBiAG74S9_dZ)

The output was extremely distorted, and did not look like a comic-book style at all.

Attempt 2: pix2pix 2d to 3d image
For the second attempt, I tried using pix2pix instead of style transfer. For the dataset, I found a comic book that had an 'original' version with pictures that were not much better than hand-drawn sketches, and a 'new' version with pictures that were higher quality and more detailed. While these two versions were not exact matches, there were some parts where similar scenes were depicted in both. Some examples: ![1](https://drive.google.com/open?id=1_yxapCnB5fy6y1n0zJe8PolRhzYXACk7), ![2](https://drive.google.com/open?id=1e-W7WrT84gbzbcQaBE3Efcvx873j-fKO).

However, training on this dataset did not yield good results. This is an example input, output, and target: ![output](https://drive.google.com/open?id=1i-LBuHj20aaEfY8b09F7Ai1_jGYJpdng). The output usually had very little resemblance to the input. After looking back at the dataset, I realized that this was most likely because the target output had very little resemblance to the input. Although they depicted similar 'scenes', there was actually very little resemblance between the input and target, and there were no patterns for how the input could be converted into the target. Based on this, I decided to try a slightly different approach for my third attempt.

Attempt 3: pix2pix 2d to 2d image
For the third attempt, I decided to focus on a different way to improve sketches than turning them into '3d' drawings. Rather than making sketches 3d, I focused on augmenting the sketches with additional details to make them more realistic but still in a comic-book style. To do this, I took the panels from the comic-books and produced a new image by performing canny edge-detection on the image. The edges were passed as the input, with the original panel from the comic-book as the target. The edge-detection removed a lot of details from the images, such as color and shading. 

