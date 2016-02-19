from machine import Timer
from machine import Pin
import BlynkLib
from network import WLAN

WIFI_SSID  = 'YOUR_WIFI_SSID'
WIFI_AUTH  = (WLAN.WPA2, 'YOUR_WIFI_PASSORD')
BLYNK_AUTH = 'YOUR_BLYNK_AUTH'

# connect to WiFi
wifi = WLAN(mode=WLAN.STA)
wifi.connect(WIFI_SSID, auth=WIFI_AUTH, timeout=5000)
while not wifi.isconnected():
    pass

print('IP address:', wifi.ifconfig()[0])

# assign GP9, GP10, GP11, GP24 to alternate function (PWM)
p9 = Pin('GP9', mode=Pin.ALT, alt=3)
p10 = Pin('GP10', mode=Pin.ALT, alt=3)
p11 = Pin('GP11', mode=Pin.ALT, alt=3)
p24 = Pin('GP24', mode=Pin.ALT, alt=5)

# timer in PWM mode and width must be 16 buts
timer10 = Timer(4, mode=Timer.PWM, width=16)
timer9 = Timer(3, mode=Timer.PWM, width=16)
timer1 = Timer(1, mode=Timer.PWM, width=16)

# enable channels @1KHz with a 50% duty cycle
pwm9 = timer9.channel(Timer.B, freq=700, duty_cycle=100)
pwm10 = timer10.channel(Timer.A, freq=700, duty_cycle=100)
pwm11 = timer10.channel(Timer.B, freq=700, duty_cycle=100)
pwm24 = timer1.channel(Timer.A, freq=700, duty_cycle=100)


def v3_write_handler(value):
    pwm9.duty_cycle(int(value))
	
def v4_write_handler(value):
    pwm10.duty_cycle(int(value))
	
def v5_write_handler(value):
    pwm11.duty_cycle(int(value))
	
def v6_write_handler(value):
    pwm24.duty_cycle(int(value))

# initialize Blynk
blynk = BlynkLib.Blynk(BLYNK_AUTH)

blynk.add_virtual_pin(3, write=v3_write_handler)
blynk.add_virtual_pin(4, write=v4_write_handler)
blynk.add_virtual_pin(5, write=v5_write_handler)
blynk.add_virtual_pin(6, write=v6_write_handler)

blynk.run()

