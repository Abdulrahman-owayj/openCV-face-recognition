# openCV
In this repositry i will walk you through the process to install opencv in windows and use it to detect faces

**First you need to install openCV:** open the powershell (you can search for it in windows).

**Then you need to follow this link to install it using pip** https://www.codingforentrepreneurs.com/blog/install-opencv-3-for-python-on-windows/

**When you end up here**
C:\> python
```ruby
 import cv2
 print(cv2.__version__)
'3.4.0' # your version may be a newer one
```
type " exit() "

**Then you can go to any editor here i will use visual studio code editor**

**Here i will write a program that will use your web camera and open a window showing your face where we will work on**

```ruby
import cv2
video_capture = cv2.VideoCapture(0)

cv2.namedWindow("Window")    #create the window

while True:
    ret, frame = video_capture.read()
    cv2.imshow("Window", frame)    #make a frame called window

    #This help you close the window by pressing 'q' key
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

video_capture.release()
cv2.destroyAllWindows()
```

save the file anywhere and name it anything but you need to remember the name and location

using the powershell go to the location you saved it in for example: c:/Users/eadh2/Desktop/ ,  ***type "cd" then write the location (cd desktop)*** 

when you reach the location write
```ruby
python NAME OF THE FILE.py
```
for example i named my file (camera test) and saved it in (desktop), **so i will write( python camera test.py)**, ***you can use the TAB button on your keyboard after writing python to help you write the file name***

**((IF you using the visual studio code you just need to press the green arrow at the top after saving the file and it will do everything for you)).**


NOW you should be seeing a window with your face on it using your front camera or webcam

**You can diplicate this line of code to have multiple windows showing your face Make sure to change the name of the window in " "**
```ruby
cv2.imshow("Window", frame)
```


## USING OPENCV TO RECOGNISE FACES

**First you need to go to powershell (search for it in the search bar) and write these lines (one after another with pressing enter after each line)**
```ruby
python
```
```ruby
import cv2
```
```ruby
print(cv2.__file__)
```

After that you will have the location of  all cascades files like this
```ruby
C:\Users\eadh2\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.9_qbz5n2kfra8p0\LocalCache\local-packages\Python39\site-packages\cv2\cv2.cp39-win_amd64.pyd
```

you need to copy the path **without the last part** like this
```ruby
C:\Users\eadh2\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.9_qbz5n2kfra8p0\LocalCache\local-packages\Python39\site-packages\cv2
```

**Now open file explorer and paste the path on the top bar to go there**
You will find file called **data** copy it to the same file where you have your python project file, so if you have your files in desktop just put the data file there

**The code used to recognise faces**
```ruby
import numpy as np                                                                                                  #import numpy and give it shortcut
import face_recognition as fr                                                                                       #import face_recognition and give it shortcut 
import cv2                                                                                                          #import cv2 
video_capture = cv2.VideoCapture(0)                                                                                 #take the video stream from the web camera

myImage = fr.load_image_file("C:/Users/eadh2/Desktop/openCV projects/me.JPEG")                                      #use this image to train the model to recognise someone you can add more to recognise more people
myImage_encoding = fr.face_encodings(myImage)[0]                                                                    #this is used if you have more than one person in your training image (0) is the numper of face in the image

known_face_encoding = [myImage_encoding]                                                                            # to encode the image and the face in it
known_face_name = ["Abdoh"]                                                                                         # give the face a name

while True:

  ret, frame = video_capture.read()                                                                                 #take a frame from the camera stream

  rgb_frame = frame [:, :, ::-1]                                                                                    #to change the colors to RGB
  face_locations = fr.face_locations(rgb_frame)                                                                     #find the location of the faces in the frame taken
   
  face_encodings = fr.face_encodings(rgb_frame, face_locations)                                                     #to encode the faces detected in the frame

  for (top, right, bottom, left), face_encodings in zip(face_locations, face_encodings):                            #to compare the faces found with the pre-trained faces 
    matches = fr.compare_faces(known_face_encoding, face_encodings)                                                 #check to see if there is a match or not

    name = "Unknown"
    face_distance = fr.face_distance(known_face_encoding, face_encodings)                                           #this will compare each face in the frame with the pre-trained faces and gives u a number of how similar to each known face

    best_match_index = np.argmin(face_distance)                                                                     #if there is a match then we determind it match with what face (the index number of the face)

    if matches[best_match_index]:
     name= known_face_name[best_match_index]                                                                        #the variable name will have the name of the best match

    cv2.rectangle(frame, (left, top), (right, bottom), (0, 0, 255), 2)                                              #draw a rectangular shape around the face 

    cv2.rectangle(frame, (left, bottom -35), (right, bottom), (0,0, 255), cv2.FILLED)                               #draw a small rectangle filled with color to write the name there
    font = cv2.FONT_HERSHEY_SIMPLEX                                                                                 #choose the font style
    cv2.putText(frame, name, (left +6, bottom -10), font, 1.0, (255, 255, 255), 1)                                  #show the name of the person

  cv2.imshow('webcame', frame)                                                                                      #Finally show the image to the user with the name attached

 
  if cv2.waitKey(1) & 0xFF == ord('q'):                                                                             #use the letter 'q' to close the camera window
   break

video_capture.release()                                                                                             # to release the software and hardware
cv2.destroyAllWindows()

```

**Make sure you use clear image of your face so it can learn it properly**


![image](https://user-images.githubusercontent.com/5675794/127233327-f6b7c402-8f1f-488a-8cde-c9da6b4a54a9.png)
