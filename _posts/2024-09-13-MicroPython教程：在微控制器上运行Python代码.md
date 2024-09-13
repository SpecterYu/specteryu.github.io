# MicroPython教程：在微控制器上运行Python代码

![MicroPython](https://www.micropython.org/images/micropython-logo.svg)

MicroPython是一种精简版的Python解释器，专门设计用于微控制器和嵌入式系统。由于其小巧灵活的特性，它成为了物联网及嵌入式设备编程的首选语言之一。本文将带领您了解MicroPython的基本知识，并指导您在微控制器上运行Python代码。

## 什么是MicroPython?

MicroPython是一款开源、高效且易于使用的Python解释器，可运行在微控制器和嵌入式系统上。它是通过精简Python语言的标准库来实现的，使得MicroPython的解释器大小仅为几十KB，因此可以轻松地安装在微控制器上。

MicroPython支持许多常见的Python语言功能，包括函数、类、模块、循环和条件语句等。其语法和标准Python非常相似，因此对于有Python编程经验的开发者来说，学习和使用MicroPython将变得更加容易。

## 如何安装MicroPython

安装MicroPython非常简单，并且针对各种常见的微控制器都有适配版本。以下是在常见微控制器上安装MicroPython的简要步骤：

1. 使用USB数据线将微控制器连接到计算机。
2. 下载适用于您的微控制器模型的MicroPython固件。
3. 将固件烧录到微控制器的闪存中。
4. 连接到微控制器的串口终端，并开始编写和执行Python代码。

## 第一个MicroPython程序

现在我们来编写和执行一个简单的MicroPython程序，以确保您的安装过程正确无误。

```python
print("Hello, MicroPython!")
```

将上述代码保存为`hello.py`文件，然后通过串口终端连接到微控制器。在终端中执行以下命令来运行程序：

```
$ python hello.py
```

您将看到输出`Hello, MicroPython!`，这意味着您已成功在微控制器上运行了第一个MicroPython程序。

## 访问硬件资源

MicroPython提供了许多内置模块和函数，以便于访问和控制微控制器的硬件资源，如GPIO引脚、SPI总线、I2C总线和ADC等。以下是一些常用硬件资源的例子：

### 控制LED灯

```python
import machine

led = machine.Pin(2, machine.Pin.OUT)  # 连接到GPIO引脚2
led.value(1)  # 打开LED
```

### 读取传感器值

```python
import machine

sensor = machine.ADC(0)  # 连接到ADC引脚0
value = sensor.read()  # 读取传感器的值
```

### 通信协议

```python
import machine
import ssd1306

i2c = machine.I2C(scl=machine.Pin(5), sda=machine.Pin(4))  # 连接到I2C总线
display = ssd1306.SSD1306_I2C(128, 64, i2c)
display.text("Hello, MicroPython!", 0, 0)
display.show()
```

## 用MicroPython构建物联网设备

MicroPython不仅可以运行简单的脚本，还可以用于构建复杂的物联网设备。通过结合Wi-Fi模块、传感器和云服务，您可以创建具有远程控制和监测功能的智能设备。以下是一个示例：

```python
import time
import network
from umqtt.simple import MQTTClient

# 连接到Wi-Fi网络
sta_if = network.WLAN(network.STA_IF)
sta_if.active(True)
sta_if.connect('your_wifi_ssid', 'your_wifi_password')
while not sta_if.isconnected():
    time.sleep(1)

# 连接到MQTT代理
client = MQTTClient('your_client_id', 'your_mqtt_broker')
client.connect()
client.publish('topic', 'Hello from MicroPython!')

# 监听来自MQTT代理的消息
def callback(topic, msg):
    print('Received message: {} in topic: {}'.format(msg, topic))

client.set_callback(callback)
client.subscribe('topic')

# 循环监听MQTT代理消息
while True:
    client.wait_msg()
```

上述代码演示了一个连接Wi-Fi网络并通过MQTT协议与云服务通信的设备。您可以根据自己的具体要求进行修改和扩展。

## 结论

MicroPython是一种强大而灵活的Python解释器，可在微控制器和嵌入式系统上运行。它使得编写和运行Python代码变得简单，同时还提供了访问和控制硬件资源的内置功能。通过MicroPython，您可以轻松构建物联网设备，为智能家居和工业自动化等领域带来更多创新。希望本教程能够帮助您入门MicroPython，并开启一段精彩的嵌入式开发之旅！
参考文献：

1. [MichroPython嵌入式开发实践之旅](https://www.jjblogs.com/post/109814)
