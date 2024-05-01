# Automated Plant Watering

The automations and such in this folder are talked about in detail in my blog post [Automated Plant Watering](https://beanbag.technicalissues.us/automated-plant-watering/).

## Automations

- [Garden Sprinklers Automation](garden-sprinklers.yaml)
- [Garden - Force Sensor Update Automation](garden-force-sensor-update.yaml)
- [Set Precipitation Likely Toggle Automation](set-precipitation-likely-toggle.yaml)

## Helpers

### Chance of precipitation in next 10 hours

Go to Settings > Devices and services > Helpers > + CREATE HELPER > Template > Template a sensor.

Make one that looks like this (the template is below for easy copy/paste):

![Screenshot of new template sensor helper](Chance-of-precipitation-in-next-10-hours.png)

Here is the code for the state template:

```python
{{ state_attr(
    'sensor.weather_forecast_hourly', 'forecast')[:10] 
    | map(attribute='precipitation_probability') 
    | list | max }}
```

It gets the next 10 hourly forecasts, pulls out the attribute called `precipitation_probability`, converts them to a list (aka an array), and then gets the largest (highest percentage) one.

### Precipitation likely between 7 & 5

Go to Settings > Devices and services > Helpers > + CREATE HELPER > Toggle.

Make one that looks like this:

![Screenshot of new toggle helper](Precipitation-likely-between-7-and-5.png)
