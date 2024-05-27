# Ultimatesensor - CO2 Colors Blueprint

This blueprint automates the color of an RGB light based on CO2 levels measured by a CO2 sensor. The light will change color depending on the CO2 concentration and optionally turn off after a set delay. This automation runs at a specified interval during active hours.

## Blueprint Overview

- **Name**: Ultimatesensor - CO2 Colors
- **Description**: Automates the RGB light based on CO2 sensor values with optional light off.
- **Domain**: `automation`

## Input Variables

- **`co2_sensor`**:
  - **Name**: CO2 Sensor
  - **Description**: The CO2 sensor to monitor.
  - **Selector**: 
    - `entity`:
      - `domain`: `sensor`
  
- **`rgb_light`**:
  - **Name**: RGB Light
  - **Description**: The RGB light to control.
  - **Selector**: 
    - `entity`:
      - `domain`: `light`
  
- **`light_off`**:
  - **Name**: Light Off
  - **Description**: Option to turn off the light after the delay.
  - **Default**: `true`
  - **Selector**: 
    - `boolean`:
  
- **`check_interval`**:
  - **Name**: Check Interval
  - **Description**: Interval to check CO2 levels (in minutes).
  - **Default**: `5`
  - **Selector**: 
    - `number`:
      - `min`: `1`
      - `max`: `60`
      - `unit_of_measurement`: `minutes`
  
- **`active_hours_start`**:
  - **Name**: Active Hours Start
  - **Description**: Time to start monitoring.
  - **Default**: `"08:00:00"`
  - **Selector**: 
    - `time`:
  
- **`active_hours_end`**:
  - **Name**: Active Hours End
  - **Description**: Time to stop monitoring.
  - **Default**: `"23:00:00"`
  - **Selector**: 
    - `time`:

## How It Works

1. **Trigger**:
   - The automation triggers every specified number of minutes (`check_interval`).

2. **Condition**:
   - The automation only runs during the specified active hours (`active_hours_start` to `active_hours_end`).

3. **Action**:
   - Depending on the CO2 level, the RGB light will change to a specific color:
     - **350 - 600 ppm**: Blue (`[0, 0, 255]`)
     - **600 - 800 ppm**: Cyan (`[0, 255, 225]`)
     - **800 - 1000 ppm**: Green (`[0, 200, 0]`)
     - **1000 - 1200 ppm**: Lime (`[135, 245, 77]`)
     - **1200 - 2000 ppm**: Orange (`[250, 175, 0]`)
     - **2000 - 5000 ppm**: Red flashing (`[250, 0, 0]`)
   - The light will stay on for 15 seconds, and then turn off if the `light_off` option is enabled.

## Example Usage

1. **Setup**:
   - Add this blueprint to your Home Assistant instance.
   - Create a new automation using this blueprint.
   
2. **Configuration**:
   - Select your CO2 sensor.
   - Select your RGB light.
   - Set the desired check interval (default is 5 minutes).
   - Define your active hours for monitoring CO2 levels.
   - Choose whether you want the light to turn off after displaying the color.

## Installation

1. Go to the Blueprints section in Home Assistant.
2. Click on "Import Blueprint" and paste the following URL: https://github.com/Diondk/homeassistant-blueprints/blob/main/Ultimatesensor%20blueprints/ultimatesensor_co2_colors.yaml
3. Click "Preview" and then "Import Blueprint".
4. Create a new automation using this blueprint and configure the input variables.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
