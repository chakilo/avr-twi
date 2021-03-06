# amg8853

AMG8853 driver for ATMega 64 (or any other Atmel AVR MCU)

## Example

```c
#include "amg8853.h"

int main(void) {

    // initializes driver
    amg8853_init();

    // initializes buffer
    uint8_t amg8853_read_data_buff[128];

    // read data
    amg8853_twi_read_64_tem(amg8853_read_data_buff);

    // initializes result
    uint8_t sign, celsius_temperature_integer_part, celsius_temperature_decimal_part;

    // temperature convert
    uint8_t i;
    for (i = 0; i < 64; i++) {
        amg8853_tem_convert(amg8853_read_data_buff, i, 
            &sign, &celsius_temperature_integer_part, &celsius_temperature_decimal_part);
        
        // do something
        
    }

    return 0;
}
```

## API

###### `void amg8853_init()`

Initializes the driver.  Should be called once before reading data from amg8853.

###### `void amg8853_twi_read_64_tem(uint8_t buff[])`

Receive 128 bytes data from amg8853 using twi.

* `buff` - buffer. 128 bytes. Should be initialized before calling this function.

###### `void amg8853_tem_convert(uint8_t buff[], uint8_t snumber, uint8_t *sign, uint8_t *integer_part, uint8_t *decimal_part)`

Convert the data to Celsius temperature.

* in
    * `buff` - data from amg8853. 128 bytes.
    * `snumber` - sensor index 0~63

* out
    * `sign` - sign of the result 1:negative, 0:positive
    * `integer_part` - integer part of the result 0~255
    * `decimal_part` - decimal part of the result (multiply by 100) 0~99

## Definitions

* `F_CPU` - should be defined as the CPU Clock frequency
* `AMG8853_DELAY` - not used
* `AMG8853_TEM_START_ADDR` - start address of temperature registers. do not need to modify
* `AMG8853_SENSOR_ADDR` - 0b1101000 or 0b1101010
* `AMG8853_WRITE` - not used
* `AMG8853_READ` - not used
