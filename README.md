# Horizontal line state card for [Home Assistant](https://home-assistant.io)
Used to separate entities in a Home Assistant group 

<img align="left" src="https://i.imgur.com/mQiMmGg.jpg" height="350">

***
***
## Features
* Highly customizable: width, thickness, borders, images, color, dashes, double lines etc.
* More than one can be added to the interface.
* Disabled more-info card.
***
KNOWN PROBLEMS: Not all options exposed in the `customize` section.
***
***
## Installation
* Download `/www/custom_ui/state-card-hline.html` and `/www/custom_ui/state-card-hline_es5.html` to `<your-hass-configuration-dir>/www/custom_ui/` (create the folder structure if you don't have it - mind the permissions)
* Add it to your `configuration.yaml`:
```yaml
frontend:
  extra_html_url:
    - /local/custom_ui/state-card-hline.html
  extra_html_url_es5:
    - /local/custom_ui/state-card-hline_es5.html
```
* Create one or more sensors, binary_sensor(s), input_text(s) etc. in your `configuration.yaml`. 
If you plan to use only one design for you horizontal line just create one sensor and use it in the groups you want.
```yaml
sensor:
  - platform: template
    sensors:
      hline_1:
        value_template: hline
      hline_2:
        value_template: hline
```
* Add your sensor to a group between the entities you would like to split E.g.:
```yaml
group:
  your_group:
    name: ' '   > in this format the chart will not have a name above (recommeded)
    entities:
      - sensor.1
      - sensor.hline_1
      - sensor.2   
      - sensor.hline_2
```
```diff
- Create more lines if you want to insert more than one in a group (a line acts like a sensor: can't be repeated more than once in a group). 
```
* Convert your newly created sensor (or an existing one that you don't use) to a horizontal line in the `customize` section or your `customize.yaml` file:

```yaml
  customize:
    sensor.hline_1:
      custom_ui_state_card: state-card-hline
    sensor.hline_2:
      custom_ui_state_card: state-card-hline
 ```
 or in the `customize_glob.yaml` file:
 ```
     sensor.hline_*:
      custom_ui_state_card: state-card-hline
 ```
 * Customize your horizontal line in the `customize` section or the `customize.yaml` file:
 ```diff
 - The config options are more or less CSS, so the combination matters in the final result!
 ``` 
 ```yaml
     sensor.hline_1:
      custom_ui_state_card: state-card-hline
      config:
        width: 90 --> in percents
        height: 0 --> in pixels, adds to bordertop
        backgroundcolor: white
        bordertop: '1px solid black'
    sensor.hline_2:
      custom_ui_state_card: state-card-hline
      config:
        width: 90 --> in percents
        height: 0 --> in pixels, adds to bordertop
        backgroundcolor: white
        bordertop: '1px dashed red'
    sensor.hline_3:
      custom_ui_state_card: state-card-hline
      config:
        width: 65 --> in percents
        height: 0 --> in pixels, adds to bordertop
        backgroundcolor: white
        bordertop: '2px double green'
    sensor.hline_4:
      custom_ui_state_card: state-card-hline
      config:
        width: 85 --> in percents
        height: 1 --> in pixels, adds to bordertop
        backgroundcolor: white
        bordertop: none
        backgroundimage: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0))
 ```
 ```
 default values:
       config:
        width: 90
        height: 0
        backgroundcolor: white
        bordertop: '1px solid black'
        backgroundimage: none
 ```
## Changelog
```diff
Version 20180211:
+Fixed a couple of bugs in the CSS.
Version 20180215:
+Added ES5 file.
On 20180418:
+Updated installation instructions
```

Some ideas for customizing:
* https://codepen.io/ibrahimjabbari/pen/ozinB
* https://css-tricks.com/examples/hrs/
