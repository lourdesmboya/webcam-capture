# webcam-capture-driver-ipcam

This is IP camera driver for Webcam Capture project. It allows Webcam Capture to
handle pictures from IP cameras supporting JPEG and MJPEG (Motion JPEG) compression
and therefore can work in two modes - ```PULL``` for JPEG and ```PUSH``` for MJPEG.

What are the differences between those two modes:

* ```PULL``` - will request new JPEG image each time when it is required,
* ```PUSH``` - stream Motion JPEG in real time and serve newest image on-demand.

Support for few IP cameras is build in and the list includes:

* [IP Robocam 641](http://www.marmitek.com/en/product-details/home-automation-security/ip-cameras/ip-robocam-641.php) by [Marmitek](http://www.marmitek.com/) (MJPEG)
* [Speed Dome X104S](http://www.ipcctv.com/product.php?xProd=10&xSec=26) by [Xvision](http://www.ipcctv.com/) (MJPEG)
* [B7210](http://www.zavio.com/product.php?id=45) by [Zavio](http://www.zavio.com/) (JPEG)
* [F3201](http://www.zavio.com/product.php?id=28) by [Zavio](http://www.zavio.com/) (JPEG)

## Code Examples

Example of  how to display image from B7210 bullet IP camera by [Zavio](http://www.zavio.com/product.php?id=45)
in ```JPanel``` inside ```JFrame``` window ([QVGA](http://en.wikipedia.org/wiki/Graphics_display_resolution#QVGA_.28320.C3.97240.29) 
image size is used).

```java
IpCamDevice ipcam = new B7210("B7210", "114.32.216.24");
ipcam.setAuth(new IpCamAuth("demo", "demo"));
ipcam.setSize(B7210.SIZE_QVGA);
		
IpCamDriver driver = new IpCamDriver();
driver.register(ipcam);

Webcam.setDriver(driver);

WebcamPanel panel = new WebcamPanel(Webcam.getDefault());
panel.setFPS(0.5); // 1 frame per 2 seconds

JFrame f = new JFrame();
f.add(panel);
f.pack();
f.setVisible(true);
f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

Example of how to handle image from *any* IP camera supporting JPEG compression:

```java
String address = "http://www.dasding.de/ext/webcam/webcam770.php?cam=1";
IpCamDevice livecam = new IpCamDevice("dasding", new URL(address), IpCamMode.PULL);

IpCamDriver driver = new IpCamDriver();
driver.register(livecam);

Webcam.setDriver(driver);

WebcamPanel panel = new WebcamPanel(Webcam.getWebcams().get(0));
panel.setFPS(5);

JFrame f = new JFrame("Dasding Studio Live IP Camera");
f.add(panel);
f.pack();
f.setVisible(true);
f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

Example of how to handle image from *any* IP camera supporting MJPEG compression. 
Here we are handling stream from the beach of Lignano (Italy) from an AXIS 213 
PTZ Network Camera.

```java
String address = "http://88.37.116.138/mjpg/video.mjpg ";
IpCamDevice livecam = new IpCamDevice("Lignano Beach", new URL(address), IpCamMode.PUSH);

IpCamDriver driver = new IpCamDriver();
driver.register(livecam);

Webcam.setDriver(driver);

WebcamPanel panel = new WebcamPanel(Webcam.getWebcams().get(0));
panel.setFPS(1);

JFrame f = new JFrame("Live Views From Lignano Beach (Italy)");
f.add(panel);
f.pack();
f.setVisible(true);
f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


