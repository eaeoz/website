+++
title = "FreeCAD Rotate Macro"
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
