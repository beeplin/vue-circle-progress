# vue-circle-progress

A circle progress component. Forked from [v-circle](https://github.com/qddegtya/v-circle) and updated with vue 2.

## Usage

```html
<circle-progress
  color="darkturquoise"
  width=140
  font-size=24
  pv="24"
  text-color="darkgray"
  bold="45"
  text-bg-color="white"
  border-color="gray"
  during=2
  bg-color="lightgray"></circle-progress>
```

## Props

```txt
prop        type     description                               example   default value

color       String   circle progress fill color                #000000   #2ecc71
width       Number   circle size                               180       150
fontSize    Number   circle progress value size                64        64
pv          Number   circle progress value                     75        0
textColor   String   circle progress value color               #bdc3c7   #bdc3c7
bold        String   circle progress outline width             10        5
textBgColor String   circle progress value background-color    #000000   #f9f9f9
borderColor String   circle progress outline color             #000000   #bdc3c7
during      Number   circle progress animation duration-time   2         0.8
bgColor     String   circle progress background-color          #000000   #f0f0f0
```

