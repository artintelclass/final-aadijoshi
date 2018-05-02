# Final

## Download
The model can be downloaded from [here](https://drive.google.com/open?id=1Qkc6AV_go3XApkRrCN5VGR4NjXMYt1QH)

## Usage
In the command-line: 'python cam.py'
Press s when the program is running and an output image will be generated for that frame

## Introduction
The goal of this project was to create a tool that could assist comic book creators visualize what a rough sketch would look like once it was improved and generated on the computer. This would be extremely useful during the brainstorming phase, for example. Instead of having to produce a detailed sketch, or having to use a graphics editor, the author could create a rough sketch and then get an idea of what the final product would look like.

## Process
### Attempt 1: Style transfer
The first idea I had was to use style transfer. The sketch that is provided as input could be seen as the 'edges' of a photo after edge detection. For example, the sketch of a city skyline and a photo of a city skyline, after it passes through an edge-detection algorithm, would be similar. Given an input image, then, the goal would be to find a similar image in the database, apply style transfer to the image, and output the new image. Furthermore, the input image could be broken down into smaller 'layers' that would be decided by the user. If an image consists of a house and car, rather than looking for similar images in the database, an output image could be created by applying style transfer to a house and a car seperately, then layering them together.

The advantage of this method was that it could turn a two-dimensional sketch into a more realistic 'three-dimensional' one. For example, a building could be drawn as a rectangle on paper. After the image passes through the program, a photo of a real building would be outputted, although style transfer would be applied to this photo.

After testing out style transfer on a photo, however, I decided to drop this idea. The result of applying a 'comic' style transfer to a city skyline can be seen here: ![result](https://drive.google.com/open?id=18bUdAK_2APMa_usko24DBiAG74S9_dZ)

The output was extremely distorted, and did not look like a comic-book style at all.

### Attempt 2: pix2pix 2d to 3d image
For the second attempt, I tried using pix2pix instead of style transfer. For the dataset, I found a comic book that had an 'original' version with pictures that were not much better than hand-drawn sketches, and a 'new' version with pictures that were higher quality and more detailed. While these two versions were not exact matches, there were some parts where similar scenes were depicted in both. Some examples: ![1](https://drive.google.com/open?id=1_yxapCnB5fy6y1n0zJe8PolRhzYXACk7), ![2](https://drive.google.com/open?id=1e-W7WrT84gbzbcQaBE3Efcvx873j-fKO).

However, training on this dataset did not yield good results. This is an example input, output, and target: ![output](https://drive.google.com/open?id=1i-LBuHj20aaEfY8b09F7Ai1_jGYJpdng). The output usually had very little resemblance to the input. After looking back at the dataset, I realized that this was most likely because the target output had very little resemblance to the input. Although they depicted similar 'scenes', there was actually very little resemblance between the input and target, and there were no patterns for how the input could be converted into the target. Based on this, I decided to try a slightly different approach for my third attempt.

### Attempt 3: pix2pix 2d to 2d image
For the third attempt, I decided to focus on a different way to improve sketches than turning them into '3d' drawings. Rather than making sketches 3d, I focused on augmenting the sketches with additional details to make them more realistic but still in a comic-book style. To do this, I took the panels from the comic-books and produced a new image by performing canny edge-detection on the image. The edges were passed as the input, with the original panel from the comic-book as the target. The edge-detection removed a lot of details from the images, such as color and shading. Since the target had all of these details, the model had to learn how to add these details to the edge-detection image. Furthermore, an image after edge-detection is similar to a sketch after edge-detection, since it mainly outlines the important parts of the image. Therefore, the edges of a sketch could be used as input to the model, and it should produce an output with additional details, such as color and shading.

While the difference between an input sketch and output image was not as drastic in this version, the effect was definitely better than any of the previous versions. Furthermore, this version succeeded in the original goal of 'augmenting' a simple sketch with additional details. An example of the output can be found here: ![output](https://drive.google.com/open?id=1QOGgTkUIK120WYGt4b_Xdhq3eepWhUzJ). The output image has some shading near the shirt collar, giving a slightly 3d effect, and also has some shading along the ear and nose. While the output was not perfect, it was potentially usable for somebody who wanted to see what the sketch would look like if it was made on a graphics editor.

### Program format
Since I had a model that was effective, I had to decide on the format for delivering access to the model. Originally my plan was to create a website where a user could upload an image and get back the output. However, this did not seem very user friendly, since somebody would have to create their sketch, scan it, upload it to the website, and finally get back a result.

An alternative was to use webcam-pix2pix-tensorflow. This allowed a live stream for a webcam to be evaluated by the model, and the output was also produced in real-time. This seemed like a much better alternative, since a user could see the changes on the computer at the same time that they were producing the sketch.

While webcam-pix2pix-tensorflow seemed like the best choice, there were problems in getting the model to work correctly with the library. The model that was made in attempt 3 couldn't work, so a new model was trained using Memo's (the creator of webcam-pix2pix-tensorflow) version of pix2pix. However, this new model did not work either.

Since webcam-pix2pix-tensorflow did not work, I wrote an alternative python script. This script captures input from the webcam when a particular key is pressed, performs edge detection on the input, sends the new input to the model, and finally shows the output produced by the model on the screen. While this program worked, it was not as seamless or fast as webcam-pix2pix-tensorflow. As such, the current goal for this project is to make it compatible with webcam-pix2pix-tensorflow.
