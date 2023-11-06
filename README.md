# EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER

### Aim:
To generate a PWM wave at the timer pin output and  simuate it on  proteus using an virtual oscilloscope  

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

The timer modules can operate a variety of modes one of which is the PWM mode. Where the timer gets clocked from an internal source and counts up to the auto-reload register value, then the output channel pin is driven HIGH. And it remains until the timer counts reach the CCRx register value, the match event causes the output channel pin to be driven LOW. And it remains until the timer counts up to the auto-reload register value, and so on.

The resulting waveform is called PWM (pulse-width modulated) signal. Whose frequency is determined by the internal clock, the Prescaler, and the ARRx register. And its duty cycle is defined by the channel CCRx register value. The PWM doesn’t always have to be following this exact same procedure for PWM generation, however, it’s the very basic one and the easier to understand the concept. It’s called the up-counting PWM mode. We’ll discuss further advanced PWM generation techniques as we go on in this series of tutorials.

The following diagram shows you how the ARR value affects the period (frequency) of the PWM signal. And how the CCRx value affects the corresponding PWM signal’s duty cycle. And illustrates the whole process of PWM signal generation in the up-counting normal mode.

STM32 Timers – PWM Output Channels

Each Capture/Compare channel is built around a capture/compare register (including a shadow register), an input stage for capture (with a digital filter, multiplexing, and Prescaler) and an output stage (with comparator and output control). The output stage generates an intermediate waveform which is then used for reference: OCxRef (active high). The polarity acts at the end of the chain.
![image](https://github.com/Reebak04/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/118364993/cfb6fef3-2b44-4fc1-9329-78152c84c171)


STM32 Timers In PWM Mode

Pulse width modulation mode allows generating a signal with a frequency determined by the value of the TIMx_ARR register and a duty cycle determined by the value of the TIMx_CCRx register. The PWM mode can be selected independently on each channel (one PWM per OCx output) by writing 110 (PWM mode 1) or ‘111 (PWM mode 2) in the OCxM bits in the TIMx_CCMRx register. The user must enable the corresponding preload register by setting the OCxPE bit in the TIMx_CCMRx register, and eventually the auto-reload preload register by setting the ARPE bit in the TIMx_CR1 register.

OCx polarity is software programmable using the CCxP bit in the TIMx_CCER register. It can be programmed as active high or active low. For applications where you need to generate complementary PWM signals, this option will be suitable for you.

In PWM mode (1 or 2), TIMx_CNT and TIMx_CCRx are always compared to determine whether TIMx_CCRx≤TIMx_CNT or TIMx_CNT≤TIMx_CCRx (depending on the direction of the counter).

The timer is able to generate PWM in edge-aligned mode or center-aligned mode depending on the CMS bits in the TIMx_CR1 register.
STM32 PWM Frequency

In various applications, you’ll be in need to generate a PWM signal with a specific frequency. In servo motor control, LED drivers, motor drivers, and many more situations where you’ll be in need to set your desired frequency for the output PWM signal.

The PWM period (1/FPWM) is defined by the following parameters: ARR value, the Prescaler value, and the internal clock itself which drives the timer module FCLK. The formula down below is to be used for calculating the FPWM for the output. You can set the clock you’re using, the Prescaler, and solve for the ARR value in order to control the FPWM and get what you want.

STM32 PWM Frequency Formula - STM32 PWM Frequency Equation
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/aca8a20e-9b99-40c1-bada-f31accaa2ae9)

STM32 PWM Duty Cycle

In normal settings, assuming you’re using the timer module in PWM mode and generating PWM signal in edge-aligned mode up-counting configuration. The duty cycle percentage is controlled by changing the value of the CCRx register. And the duty cycle equals (CCRx/ARR) [%].
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/58ce0807-331e-49f7-bc8d-373f82592a92)

## STM 32 CUBE PROGRAM :
```
Developed by : Tejusve Kabeer.F Register no : 212222100054
HAL_TIM_Base_Start(&htim2);
HAL_TIM_PWM_Init(&htim2);
HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_1);
```
## Output screen shots of proteus  :
## CIRCUIT DIAGRAM : 
 ![image](https://github.com/Reebak04/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/118364993/28273f21-c74f-45ec-9f8e-33a1b49221e6)

## DUTY CYCLE AND FREQUENCY CALCULATION 
### FOR PULSE AT 1200
![image](https://github.com/Reebak04/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/118364993/7b8fca40-6a74-490d-8be0-48a65ef2fb0a)


TON = 2.5*0.2 = 0.5

TOFF= 6.5*0.2 = 1.3

TOTAL TIME = 0.5+1.3 = 1.8

FREQUENCY = TON/(TOTAL TIME)*100 = 0.5/1.8*100=27.7%%

### FOR PULSE AT 1500

![image](https://github.com/Reebak04/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/118364993/d3bb3e2e-85bb-498b-b457-3e9a9fcf02a8)


TON = 0.5*2 = 1

TOFF= 0.5*1.5 = 0.75

TOTAL TIME = 1+0.75 = 1.75

FREQUENCY = 1/1.75*100 = 57%


### FOR PULSE AT 800

![image](https://github.com/Reebak04/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/118364993/06e1c4d0-7a37-4799-9beb-5a9a239e274c)

TON = 0.2*2 = 0.4

TOFF= 0.2*7 = 1.4

TOTAL TIME = 0.4+1.4 = 1.8

FREQUENCY = 0.4/1.8*100 = 22.22%


## Result :
A PWM Signal is generated using the following frequency and various duty cycles are simulated 




