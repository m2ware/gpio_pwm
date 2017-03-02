# gpio_pwm 

Command line utility for software PWM control of Raspberry Pi GPIO pins.

This program pulses a gpio pin with a PWM signal.  It uses nanosleep between
cycles, requiring very little CPU bandwidth.  Can be used for simple PWM projects.

Because it is software PWM, timing depends on Linux system.  While it is likely
to become unreliable for applications requiring very precise timing, it works
quite well for things like LED intensity controls and servo motor applications.  
It is possible that timing accuracy may suffer when the CPU is heavily loaded.  
However, I've used it successfully in numerous servo applications (most of which 
involve steering camera mounts).

If your project requires very fine precision (anything shy of 50us, give or take)
or has safety concerns of any sort regarding its operation, this utility should 
not be used.  Don't try to fly a quad-copter with it.  

Note that the utility simply sends a pulse train and then exits, so may not be
suitable for applications for which a constant on-station signal needs to be
provided.  Planned future enhancements will allow for continuous signalling with
the ability to change position with subsequent commands.

Usage:

    gpio_pwm [pin] [pulseDuration] [repCount] [dutyCycle]
    
    pin is the GPIO pin number
    pulseDuration is specified in microseconds (T_cycle)
    repCount is a positive integer
    dutyCycle is an floating-point percentage from 0 to 100 (controls pulse width)

Example:

    >> gpio_pwm 18 10000 100 15
    
    will send 100 pulses with 1500us duration (15% duty cycle on a 10,000us
    pulse period, corresponding to 100hz).  This will send most servo motors
    to neutral/center position.


