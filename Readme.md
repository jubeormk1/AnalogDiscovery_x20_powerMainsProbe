# ADVISE: This project is a work in progress

This is the first version of the instruments. Please review and make constructive comments about the design. Use under your own risk for evaluation purposes only. After my internal validation the an "Stable version will be release." After I get this right more board to improve the versatility of the great [AnalogDiscovery board by Agilent](https://analogdiscovery.com/) will be release.

# Introduction

<img src="https://github.com/jubeormk1/AnalogDiscovery_x20_powerMainsProbe/blob/master/output/Assembled%20photo.jpeg" width="50%"/>

This is a design initially created to look a the shape of mains outlets. I design it to check the total harmonic distortion of a generator outlet with a x20 reduction.

It has two inlets to measure two active line with the same neutral, i.e. the signal before and after a power line filter. It is intended to measure only voltage up to a frequency of at least 100kHz without a significant reduction of the signal (under 3db).

The connector is made to be connected to an Analog Discovery Digilent Instrument. It has been design to compensate the internal impedance of this particular instrument (1MOhm, 24pF). If you have one of these you can tune it so it works at it's best.

So far the version v0.1 has been release with some issues. This issues are related with the PCB layout, mainly related to the main connector pins and an unconnected pin. Apart from that the measured frequency response tested with flying wires is a success as you can see in the next frequency response analysis.

<img src="https://github.com/jubeormk1/AnalogDiscovery_x20_powerMainsProbe/blob/master/tests/06_Channel_two_frecuential_response.png" width="100%"/>

The frequential response is almost flat with a small deviation only 0.39dB at 100kHz. The phase shift is kept close to zero for the whole analysis from 10Hz to 400kHz with an increasing positive slope from 400kHz ending under 5 degrees.

# Warnings

* This circuit is intended to be use to measure monophasic power mains up to 240Vrms. Such a voltage imply electric risk and only professionals with the right skills and safety protections should use it.

* The neutral of the power outlet under test will be connected to the GND of the instruments in use. Before any use make sure that there is no connection from the GND of the instrument with the protective heart (PE) of your installation.

* If the GND of your instrument is connected to PE you should isolate it using an appropiate method, which could be an isolation transformer.

* Prior to the first use it is necessary to adjust the gain of both channels using resistor trims. See the tune procedure section in this document to understand the procedure.

* If used without a plastic case, provide adequate means to prevent accidental contact with the AC voltage present by isolating the exposed metal points.

* If unsure about above conditions are met please don't use this design.

* Use under your responsibility

* Any damage caused by the use of this design is responsibility of the licensed professional using it

# Specifications

After tuned this circuit delivered:
* Two channels connected to scope 1 and 2
* An x20 attenuation in both channels
* AC/DC coupling mode via jumpers selection in each channels
* Impedance matching to obtain an  uniform amplitude and phase frequency response from DC to at least 100kHz
* Protection for over voltage (varistor) rated to the used device


# Tune procedure

This procedure consist in two tunning procedures and a measurement of the frequency response. The order is important in this procedure. Once tunned at the circuit best. The tunning procedure is made with very low voltages (5V). This is done to prevent any damage to the board or the instrument used. If unexpected volts appear please check the components values before continuing and correct any anomaly. A visual inspection of the board is also recommended to look for short circuits, missing components or bad soldering points.

## Required equipment:
* Personal Computer
* Digilent Analog Discovery (R) Instrument
* Software Digilent Waveforms(R)
* Small isolated flat screwdriver
* Male to male connection leads
* Recommended but not required: multimeter


## Tunning the gain of a channel

Repeat this procedure for channel one and channel two.

1. Connect the jumpers of the channel under test in DC position.
2. Connect a male to male lead from GEN1 to the  in the appropriated input connector with a the pin socket corresponding to the channel under test
3. Connect the extension board to an Analog Discovery Digilent Instrument
4. Using Waveforms>Wavegen generate a DC signal in generator 1 channel of 5 Volts
5. Using Waveforms>Scope or Waveforms>Voltmeter obtain the value at the channel that you are calibrating.
6. Turn the dial on the trim resistor until you obtain 5/20 V (0.25V)

## Tunning the frequency response of a channel

Repeat this procedure for channel one and channel two. Use the channel not being tested as auxiliary channel.

1. Connect the jumpers of each channels in DC position.
2. Connect a male to male lead from GEN1 to the  in the appropriated input connector with a the pin socket corresponding to the channel under test
3. Connect a male to male lead from the channel you are not testing to GEN1
4. Connect the extension board to an Analog Discovery Digilent Instrument
5. Using Waveforms>Wavegen generate an square signal in generator 1 channel of +-5 Volts at a frequency of 10Hz
6. Using Waveforms>Scope obtain a good scope of the rising edge of the signal generated by the waveform generator and the reading in the channel you are adjusting
7. At this point you should have a signal with an amplitude of 1/20 from the channel under test to the auxiliary channel.
7. Turn the dial on the trim capacitor until you get the smaller possible raising time without overshooting.


## Measurement of the frequency response.

Repeat this procedure for channel one and channel two. Use the channel not being tested as auxiliary channel. Do this after you calibrate the gain and the frequency response. You can do it beforehand to check how wrong the probe was and compare it to an adjusted channel.

1. Connect the jumpers of each channels in DC position.
2. Connect a male to male lead from GEN1 to the  in the appropriated input connector with a the pin socket corresponding to the channel under test
3. Connect a male to male lead from the channel you are not testing to GEN1
4. Connect the extension board to an Analog Discovery Digilent Instrument

5. Using Digilent Waveforms>Network Analyser configure an acquisition from 10Hz to 10MHz and 300 samples

6. Initiate a single acquisition

7. Note down the frequency where the signal drop 3dBs from the 10Hz response. This is the bandwidth of your channel

8. Note down the phase at it's minimum and maximum values

9. Repeat the frequency response tunning until you get the best bandwidth


# License

Analog Discovery (R) and Waveforms(R) are Digilent trademarks.

The license is described in the file 'LICENSE'.
