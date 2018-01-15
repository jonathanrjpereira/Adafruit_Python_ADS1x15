# Adafruit Python ADS1x15
Python code to use the ADS1015 and ADS1115 analog to digital converters with a Raspberry Pi or BeagleBone black.

## Installation

To install the library from source (recommended) run the following commands on a Raspberry Pi or other Debian-based OS system:

    sudo apt-get install git build-essential python-dev
    cd ~
    git clone https://github.com/adafruit/Adafruit_Python_ADS1x15.git
    cd Adafruit_Python_ADS1x15
    sudo python setup.py install

Alternatively you can install from pip with:

    sudo pip install adafruit-ads1x15

Note that the pip install method **won't** install the example code.

## Analog Input Voltage Constraints
Analog input voltages must never exceed the analog input voltage limits given in the Absolute Maximum Ratings. If a VDD supply voltage greater than 4 V is used, the ±6.144 V full-scale range allows input voltages to extend up to the supply. Although in this case (or whenever the supply voltage is less than the full-scale range; for example, VDD = 3.3 V and full-scale range = ±4.096 V), a full-scale ADC output code cannot be obtained. For example, with VDD = 3.3 V and FSR = ±4.096 V, only signals up to VIN = ±3.3 V can be measured. The code range that
represents voltages |VIN| > 3.3 V is not used in this case.

## Single Ended VS Differential Inputs
The ADS1x15 breakouts support up to 4 Single Ended or 2 Differential inputs.
Single Ended inputs measure the voltage between the analog input channel (A0-A3) and analog ground (GND).
Differential inputs measure the voltage between two analog input channels.  (A0&A1 or A2&A3).

Single Ended Inputs can only measure **Positive voltages**. Without the sign bit, you only get an
effective **15 bit resolution**.
Differential inputs can measure both **Positive and Negative voltages** providing the full **16 bit
resolution**.

## Single Ended Input Voltage Measurement
Single Ended Inputs have a resolution of only 15 bits(2^15 = 32768 levels) and can measure only positive voltages.  
The Gain values determines the maximum positive voltage that can be measured whereas the supply voltage is just the physical limit of the signal you can measure without damaging the chip.

Example: If the Gain is set to 2/3, the maximum positive voltage that can be measured is 6.144V.  
*6.144/32768 = 0.0001875 V/level* . Let us call this value LSB size.  
For different Gain values we will have different maximum measureable positive voltage(Full Scale Range) & its corresponding LSB size as shown in the table.  
| Gain | Full Scale Range | LSB Size |
| --- | --- | --- |
| 2/3 | 6.144V | 0001875 = 187.5uV |
| 1 | 4.096V | 0.000125 = 125uV |
| 2 | 2.048V | 0.0000625 = 62.5uV |
| 4 | 1.024V | 0.00003125 = 31.25uV |
| 8 | 0.512V |0.000015625 = 15.625uV |
| 16 | 0.256V | 0.0000078125 = 7.8216uV |

From this we can find the value of the Input Analog Voltage for these Gain values.  
***Input Analog Voltage =  Raw Value * LSB Size***
