Explanation of our implementation:

ASSIGNMENT 4:

IPixel and Pixel:

First we created an IPixel interface and a Pixel class which are used to represent a pixel in an image. The IPixel interface has a few methods that help brighten, darken, visualize a color component, visualize the value, luma or intensity and to get the red, blue or green value of a pixel. Then, the Pixel class implements the Pixel interface and has 3 fields which represent the color components (red, green and blue). The constructor takes in these 3 variables as arguments and and checks if the values of the components are within [0,255], which would be the limits for the values of a color. If they are not, it throws an exception, because we would have an invalid color. If they are, however, it initializes the fields of the Pixel with the values passed in as arguments. The Pixel class overrides the methods provided in the interface. It changes the color values of the pixel according to the type of method( for example for visualize value it changes all the color components to the maximum value of the 3) and returns a new Pixel with the updated value ( we only made brighten and darken of type void. Thus, they will simply change the values of the Pixel- we made sure in the next steps that we use this carefully in order to not mutate our pictures when not necessary). We also implemented the equals method and the hash code in order to be able to test the equality of two Pixels properly ( we assumed that two pixels are equal if all of the color values of the first one are equal to the color values of the given pixel).


IImage and Image

We created an interface that represents an image (which is an array of pixels) called IImage and that has methods that will help execute the commands we want on the model. We added methods for getting the width or height, getting a pixel at a specific position, computing the maximum color value in the image and copying an image. We, then, created a class that implements this interface, called Image, which has one field, a 2D array of pixels. The constructor for this class takes in a 2D array of pixels and checks if it is null. If it is we throw an exception and if not, we initialize each element of the array with the values of provided argument, using a helper method. The helper method goes through the provided array and initializes each pixel of this Image with the current element in the array(we use requireNonNull to ensure that every element added to the field is not null). Then, we wrote the methods implemented by the interface. For this class, we just used the dimensions of the array and the indices to return the necessary information. We also implemented the equals method and the hash code in order to be able to test the equality of two Images properly ( we assumed that two images are equal if all of the pixels in their array are equals to the pixels in the array of the provided Image object).

ImageModel and ImageModelImpl

This is where we created our model (which is represented by a hash map of images and strings). We first made an interface ImageModel which has the methods that represent the commands that could be called by the controller, which could be: brighten, darken, flip(horizontally or vertically), visualize a color component or value, luma and intensity, which all take in as an argument a string variable that represents the key of the element we are trying to process, in the map of the model. We also added an add method and a getKey method that add an element to the current model (it takes in as arguments the name of an image and an image) and respectively return an element from the model given a key from the hash map. Our class for the model, ImageModelImpl, has 1 field which is a hash map of strings and images. This will hold all of the images we would want to keep in the model, along with their name ( which is provided by the user).This way, every time we call a method that modifies the original image we can store the new image in the hash map under a new name. Our class overrides the methods provided in the interface. For each method, it gets the element at the provided key in the map and modifies each pixel in the image, using the methods of the IPixel interface. For the flip, it simply goes through the rows and column of an image(the array of pixels) and constructs a new Image with the updated order of the elements in order to create the flip(horizontal or vertical). The methods throw appropriate exceptions if the key provided as an argument isn’t actually present in the hash map.

ICommand and the command design

In order to respect the command design pattern, we created an interface, ICommand that represents a command that can be called by the controller on the model. This interface has only one method “go”, which runs the specific command on a model which is passed in as an argument. We created 10 classes that implement this interface which represent each command that can be run on an ImageModel: Brighten, Darken, BlueComponent, GreenComponent and so on. For each of these classes, we have 1 field that represents the key of the specific image we would like to process from the model (for bright and darken we also have the values by which to brighten or darken). Then, each class overrides the go method from the interface by calling the specific method for the class on the model which is provided as an argument.

IImageController and ImageController

We first created an interface for the controller which only has one method, “go”, which runs the commands provided by the user. For the controller class, ImageController, which implements the interface, we have 4 fields, a Readable object (from where we read the commands from the user), an Appendable object, the model (which we add to using the commands provided) and the view. We use a constructor, where we check if any of the arguments are null. If they are, we throw an exception, otherwise, we initialize our fields with the provided arguments. Then, we override the go method from the interface. We do that by constantly reading the first command from the readable and using a switch case to determine which command is being called on the model. (For each switch case, we call the command that matches the provided string and we process it on a desired image and add the image to the model). We do this until there are no more commands to read from the readable. The go method throws the appropriate exceptions if there are no more values to read from the Readable object.

ImageUtil

We created two methods called loadPPM and savePPM in the provided class. The first function will load an image from a given ppm file and return an array of pixels, which we will use in the controller to create a new image. The latter one, takes in a name of the file we would want to save the image to and an image. We will go through the image and print the header “P3”, the width and the height and the values of all the pixels to the file. Lastly, we updated the main method, so that it creates a controller that reads from the terminal and prints to it and then calls the go method on that controller.


Script of commands

Our program accepts the commands:

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

brighten increment image-name dest-image-name  —The increment may be positive (brightening) or negative (darkening)


Thus a script of commands that one can introduce for our program would be:

“load res/kid.ppm Image1”

“red-component Image1 Image1R”

“horizontal-flip Image1R Imag"

"save ImageUpdate.ppm Imag"

"quit"

**We have to quit after every command so that it exits out of the loop.



The link to the source of the ppm file:

https://pixabay.com/illustrations/kids-child-small-bear-4967808/



ASSIGNMENT 5:

Filter

We created an abstract class that represents the filters that can be applied to a picture. This 
class has a constructor that takes in a kernel, which is a 2d array. The constructor throws an exception if the kernel has an even length/width or if it is null. 
The abstract class also implements a method that applies a filter to a Pixel. The method takes in an image and the coordinates of the pixel that should be blurred and applies 
the elements of the kernel to the chosen pixel and the ones surrounding it within the provided image. It returns a new Pixel that reflects the filter that was just applied.
This abstract class is extended by two classes:

- Blur: which has two constructors- a default one that has its kernel as the 3X3 Gaussian kernel and another constructor that takes in a kernel and calls super(the constructor of the abstract class).
This class inherits the applyFilter method that will apply the blur kernel on a pixel from a provided image.
- Sharpen: which has two constructors- a default one that has its kernel as the 5X5 kernel provided in the assignment instructions and another constructor that takes in a kernel and calls super(the constructor of the abstract class).
  This class inherits the applyFilter method that will apply the sharpen kernel on a pixel from a provided image.

We implemented these two filters(added methods that create instances of Blur and Sharpen and call the applyFilter method) in our IPixel, IImage and ImageModel interfaces. This way, we can easily call the methods using pixels, images or models.

Color Transformation

We created a second abstract class, ColorTrans, that represents the color transformations that can be done to a pixel. This
class has a constructor that takes in a kernel, which is a 2d array. The constructor throws an exception if the kernel is not a 3X3 (because it should be applied to the 3 color values of a pixel) array or if it is null.
The abstract class also implements a method that makes a color transformation on a pixel. The method takes in a pixel and applies the kernel on its color values (it is like a matrix x vector multiplication where the matrix is our kernel and the vector is the [r g b] values of the pixel).
It returns a new Pixel that reflects the color transformation that was just applied.
This abstract class is extended by two classes:

- GreyScale: which has two constructors- a default one that has its kernel as the 3X3 kernel provided in the assignment instructions (for greyscale) and another constructor that takes in a kernel and calls super(the constructor of the abstract class ColorTrans).
  This class inherits the applyColorTrans method that will apply the greyscale kernel on a pixel.
- SepiaTone: which has two constructors- a default one that has its kernel as the 3X3 kernel provided in the assignment instructions (for sepia) and another constructor that takes in a kernel and calls super(the constructor of the abstract class ColorTrans).
  This class inherits the applyColorTrans method that will apply the sepia-tone kernel on a pixel.

We implemented these two color transformations(added methods that create instances of GreyScale and SepiaTone and call the applyColorTrans method) in our IPixel, IImage and ImageModel interfaces. This way, we can easily call the methods using pixels, images or models.

Controller

We added the new commands to the controller adding four new cases to the switch case "blur","sharpen","greyscale","sepia-tone". For each case, we called the appropriate method from the model (the method will call either applyFilter or applyColorTrans).

Load and Save

We created new load and save functions that accept jpg, ppm, png, bmp formats in the ImageUtil class. We also, used the command design pattern for the load and save methods. We created and interface LoadSave that only takes in one method
called runLoadSave. Then, we implemented this interface in two classes that represent the load and save methods. In each class we have two fields which represent the name of the file and the key of the image in the map of the model. Within the two classes, we just
override the runLoadSave method so that it calls the appropriate methods from the ImageUtil class. 

We also updated the controller, so that it uses the command design pattern for the load and save methods.

ASSIGNMENT 6:

IImage and Image

We implemented six new methods for the IImage interface and the Image class that implements it. Three of the methods return lists of the red, green and blue values of 
an image. The next method returns a boolean value that determines if the image is greyscale. We also implemented a method and a helper for it that creates 
a list of the frequencies of the values from 0 to 255, given a list of integers. This will help us create the histograms for the color values of an image.

HistogramCol

We created a new class that creates a histogram for the current image that is being displayed. This 
histogram class has fields that represent the list of values that is being graphed (the frequency of 
certain color values), a boolean value that indicates if an image is greyscale, a color and the x and y hatches, which represent the section values of 
the x and y axis (if the y hatch is 10 then the y axis will be sectioned in 10 parts). The constructor initializes the
histogram with default values, setting the list to an empty one, the color to gray, the hatches to 10 and
the boolean value to false. In order to later update the histograms depending on our image, we created three
methods, which take in an image, called: setRedValues, setGreenValues and setBlueValues. These methods, take the image passed
as an argument and set the values of the previously described fields using the methods presented earlier (the new methods implemented in
the IImage and Image). The histogram class extends the JPanel class and overrides a method from the class: paintComponent. The paint component
draws the x and y axis, the sections determined by the hatches, the points generated from the list and the line that joins each point.

*The user can update the x and y hatches by updating the last two values in the set functions with the desired number.

GUI

The GUI class represents our GUI view. The class extends the JFrame class. Therefore, we create two panels and add them to 
the GUI. The first panel represents the image icon that shows the current image that the user can process. The second panel
is formed by three different histograms (one for each color - red, green, blue), each placed on a different row. The two panels are 
placed side by side in the GUI, with the image being on the left side and the three histograms on the right
side. Initially, our histograms are empty, since we use the default constructor in the GUI constructor. We created a new method,
displayImage that takes in an IImage and updates the three histograms using the set methods from the HistogramCol class. 
In this method, we also update the image icon so that it displays the image passed as an argument and we repaint the GUI.

In the GUI we also created a menu bar that has three options "Load", "Save" and a submenu called "Processes". The Processes
submenu has 14 options representing the commands that can be operated on an image. We added these commands as action listeners
and passed them to an object of type ActionListener, using a method called "setListener". This method will be called in the constructor of our controller.

Our view also has two methods writeMessage and createMessageBox that assures that any failed command is reported
to the user through a pop-up box that includes a message indicating the error.

The class also has a field that holds the key of the current image in the model. This helps us keep track of the image we are modifying
within the model, in the controller. For this, we also implemented two methods : returnKey and setKey that help us access and modify this
field of the view from the controller.

GUIController

Our controller implements the interface ActionListener. It takes in a model and a GUI view. In the constructor, the model and view are initialized with
the arguments and we call the setListener method of the view with the controller passed as an argument in 
order to add all the commands to the ActionListener. Then, still in the constructor, we check if the current key of
the model is null. If it is, that means that it is the start of the program and no picture has been loaded. Therefore, we 
make the user first load a picture before proceeding. Because the class implements the ActionListener interface, it has to implement the
method actionPerformed that handles each command. This method checks the action event passed as an argument and depending on the command
described in that event it calls function on the image from the model at the current key(the key is passed by the view). For example, if the
current key is "Imag1" and the action event is blur, the controller will blur the image from the hash map of the model that has the key "Imag1". Then,
it adds the updated image to the model with a new key (we usually made the new key by adding to the old one the name of the command- so in the example
it would be "Imag1 blur") and also updated the key of the view with the new one (using setKey). Lastly, we just called the displayImage method
on the view passing it the updated image.

How to use our program:

- The first thing that pops up when a user runs the program is the load window. Therefore, the user has to load an image
  in order to start using the commands of the program. The user has to choose an image to load from a file.
  If the program cannot load the image chosen by the user, it will show a message indicating that the process was not
  possible.
- After a photo was successfully loaded, the image icon will pop up on the left side of the screen and the user will be
  able to see three histograms on the right side of the screen that represent the frequencies of the values from the red, blue and green
  lists of integers.
- There will be a menu on the left top corner of the window. The user should press on the "Menu" button and they will
  be able to see a dropdown menu with three options "Load", "Save" and "Processes".
- If the user wants to load a new image, they can press on the load button and they will be asked to choose a file to load
  once again.
- If the user wants to save the image they are currently seeing, they can press save and a window will pop up, prompting them
  to choose a directory and give the name of the file they would like to save the image as. The name of the new file, will
  be introduced by the user in a box on the top center of the window.
- If the user wants to process the current image, they can press on the "Processes" button and they will see a submenu. The submenu
  contains all the modifications that could be done to the image, like Blur, Sharpen, Sepia. The user can choose to modify the image
  in any way they would like by pressing on the button that reflect their desired process. Once the user presses on the specific
  submenu option, the image will change accordingly, as well as the histograms. If the user wants to continue processing the image,
  if they press a new button from the submenu the change will be made on the picture currently displayed on the screen, not on the
  original version.
- If the user wants to quit the program, they can simply press the "x" icon in the top left corner and the window will disappear.

** Problem that we encountered:
- Whenever we try to run the program via the jar file, the load window pops up with the folders from the computer open, as it should, however,
the assignment and res files are not visible. Whereas, when we run the code through the ImageUtil, it works perfectly. We tried a few different things,
however it did not work. Also, whenever we tried to place the jar file in the res folder it would stop working, that is why we placed
it outside.

The link to the source of the ppm image:

https://pixabay.com/illustrations/kids-child-small-bear-4967808/