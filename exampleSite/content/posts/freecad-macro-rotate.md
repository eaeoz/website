+++
title = "Freecad Rotate Macro"
image = "/images/post/freecadrotate.jpg"
author = "Sedat"
date = "2025-02-08T00:02:00Z"
description = "freecad macro angle"
categories = ["FreeCAD"]
type = "post"

+++

In FreeCAD, a Python script can be used to rotate two interlocking gears by changing their angles over time using a timer. This approach enables dynamic simulation, where each gear rotates at a calculated speed based on its size and tooth ratio. By utilizing FreeCAD’s App.Timer or an external loop, the script updates the rotation incrementally, creating a smooth motion effect. This technique is valuable for visualizing mechanical movements, testing gear interactions, and automating animations within FreeCAD’s 3D workspace, making it a useful tool for engineers and designers.

***

### Example Change Angle Using Timer (rotate 2 gears)

```
from PySide import QtCore

gear20Teeth = 20
gear10Teeth = 10
gear20AngleOffset = 9
r = 0

def update():
	global gear20Teeth, gear10Teeth, gear20AngleOffset, r
	#gear10
	App.getDocument("animated_gears").Body001.Placement=App.Placement(App.Vector(-38,0,0), App.Rotation(App.Vector(0,0,1),-r), App.Vector(0,0,0))
	#gear20
	cogRotation = gear20AngleOffset + r * (gear10Teeth / gear20Teeth)
	App.getDocument("animated_gears").Body.Placement=App.Placement(App.Vector(0,0,0), App.Rotation(App.Vector(0,0,1),cogRotation), App.Vector(0,0,0))
	r+=1

timer = QtCore.QTimer()
timer.timeout.connect(update)
timer.start(1)
```

* Use `timer.stop()` from python console to stop macro.

### Additionally, Macro with Dialog Box to Start and Stop

```
from PySide import QtCore, QtGui
import FreeCAD

gear20Teeth = 20
gear10Teeth = 10
gear20AngleOffset = 9
r = 0
timer = None  # Declare the timer globally
dialog = None  # Declare the dialog globally

def update():
    global gear20Teeth, gear10Teeth, gear20AngleOffset, r
    # Update gear positions
    App.getDocument("animated_gears").Body001.Placement = App.Placement(App.Vector(-38, 0, 0), App.Rotation(App.Vector(0, 0, 1), -r), App.Vector(0, 0, 0))
    # Calculate cog rotation
    cogRotation = gear20AngleOffset + r * (gear10Teeth / gear20Teeth)
    App.getDocument("animated_gears").Body.Placement = App.Placement(App.Vector(0, 0, 0), App.Rotation(App.Vector(0, 0, 1), cogRotation), App.Vector(0, 0, 0))
    r += 1

def stop_macro():
    global timer
    if timer is not None:
        timer.stop()  # Stop the timer
        timer = None  # Clear the timer reference
        print("Macro stopped.")

def start_macro():
    global timer
    timer = QtCore.QTimer()
    timer.timeout.connect(update)
    timer.start(1)

def create_dialog():
    global dialog, cancel_button, restart_button
    # Create a dialog with cancel and restart buttons
    dialog = QtGui.QDialog()
    dialog.setWindowTitle("Animated Gears")

    layout = QtGui.QVBoxLayout()

    # Status label
    status_label = QtGui.QLabel("Animation is running...")
    layout.addWidget(status_label)

    cancel_button = QtGui.QPushButton("Cancel")
    cancel_button.clicked.connect(lambda: stop_macro_and_update_status(status_label, cancel_button, restart_button))
    layout.addWidget(cancel_button)

    restart_button = QtGui.QPushButton("Restart")
    restart_button.setVisible(False)  # Initially hide the restart button
    restart_button.clicked.connect(lambda: restart_macro(status_label, cancel_button, restart_button))
    layout.addWidget(restart_button)

    dialog.setLayout(layout)

    # Connect the dialog's finished signal to the stop function
    dialog.finished.connect(lambda: stop_macro_and_update_status(status_label, cancel_button, restart_button, True))

    dialog.show()

    # Start the macro
    start_macro()

    # Execute the dialog
    dialog.exec_()

def stop_macro_and_update_status(status_label, cancel_button, restart_button, close_dialog=False):
    stop_macro()
    status_label.setText("Macro stopped.")
    cancel_button.setVisible(False)
    restart_button.setVisible(True)

    if close_dialog:
        dialog.close()

def restart_macro(status_label, cancel_button, restart_button):
    global r
    r = 0  # Reset the rotation counter
    stop_macro()  # Stop the current macro
    status_label.setText("Animation is running...")
    cancel_button.setVisible(True)
    restart_button.setVisible(False)
    start_macro()  # Restart the macro without closing the dialog

# Start the process
create_dialog()
```
