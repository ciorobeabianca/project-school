Script commands supported by our program:

load image-path image-name

save image-path image-name

red-component image-name dest-image-name

green-component image-name dest-image-name

blue-component image-name dest-image-name

value-component image-name dest-image-name

luma-component image-name dest-image-name

intensity-component image-name dest-image-name

horizontal-flip image-name dest-image-name

vertical-flip image-name dest-image-name

brighten increment image-name dest-image-name  —The increment may be positive (brightening) or
negative (darkening)

blur image-name dest-image-name

sharpen image-name dest-image-name

greyscale image-name dest-image-name

sepia-tone image-name dest-image-name

quit


Conditions for the script commands:
- Before processing an image the user has to load it from a file. This will store the image into
  the hashmap of the model. Therefore, load will always be the first command introduced.
- After processing an image, one can save it to a new file. The user cannot save an non-existent
  picture. They would have to load and process it according to their preference and then save it to
  the desired file.
- After a user quits the game they cannot process images anymore. Thus, quit would always be the
  last command introduced.

GUI

Instructions:

- As soon as the program is started the user will be asked to load an image. The user has to choose a 
file containing an image.

To Load:
- If the user wants to load a new image they can press on the Menu and then on the Load button and a
window will pop up asking them to choose a file.

To Save:
- If the user wants to save the image they are currently looking at they can press on the Menu and then on the
Save button and a window will pop up asking them to type the name of the file they would like to save the image as
and the directory.

Processes:

To Blur
- The user has to go to: Menu->Processes->Blur

To Sharpen
- The user has to go to: Menu->Processes->Sharpen

To make it Sepia Tone
- The user has to go to: Menu->Processes->Sepia

To make it Greyscale
- The user has to go to: Menu->Processes->GreyScale

To do Green Component
- The user has to go to: Menu->Processes->Green Component

To do Blue Component
- The user has to go to: Menu->Processes->Blue Component

To do Red Component
- The user has to go to: Menu->Processes->Red Component

To do Luma Component
- The user has to go to: Menu->Processes->Luma Component

To do Intensity Component
- The user has to go to: Menu->Processes->Intensity Component

To do Value Component
- The user has to go to: Menu->Processes->Value Component

To do Horizontal Flip
- The user has to go to: Menu->Processes->Horizontal Flip

To do Vertical Flip
- The user has to go to: Menu->Processes->Vertical Flip

To Brighten
- The user has to go to: Menu->Processes->Brighten

To Darken
- The user has to go to: Menu->Processes->Darken

To quit
- A user has to press the red "x" button in the top left corner
of the screen.







