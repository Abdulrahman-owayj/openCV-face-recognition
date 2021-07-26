# openCV-face-recognition
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

**save the file anywhere and name it anything but you need to remember the name and location**

**using the powershell go to the location you saved it in for example: c:/Users/eadh2/Desktop/**,  ***type "cd" then write the location (cd desktop)*** 

**when you reach the location write**
```ruby
python NAME OF THE FILE.py
```
***for example i named my file (camera test) and saved it in (desktop)***, **so i will write( python camera test.py)**, ***you can use the TAB button on your keyboard after writing python to help you write the file name***

**((IF you using the visual studio code you just need to press the green arrow at the top after saving the file and it will do everything for you))**

**NOW you should be seeing a window with your face on it using your front camera or webcam**

**You can diplicate this line of code to have multiple windows showing your face Make sure to change the name of the window in " "**
```ruby
cv2.imshow("Window", frame)
```
