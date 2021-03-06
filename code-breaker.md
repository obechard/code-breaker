# Code Breaker
Welcome to the Code Breaker tutorial from the Canada Science and Technology Museum.
This game requires 2 players. You will be coding symbols that make up the Morse Code, a dot and a dash. You'll be able to use these symbols to send coded messages to your partner. Can you crack it?

## Set radio
To send your message, set up the radio function. 
1. In the radio tab, drag in ``||radio:radio set transmit power (7)||`` and place it in ``||basic:on start||``. 
2. Next, select the ``||radio:radio set group||`` and place it under the first radio block.

```blocks 
radio.setTransmitPower(7)
radio.setGroup(1)
```

## Create your dot
Next, code the dot. This will get sent to your partner. 
1. Drag in the ``||input:on button A pressed||`` to your workspace. 
2. Next, drag in the ``||basic:Show leds||`` and nest it in ``||input:on button A pressed||``. 
3. Select the squares you want to light up. Make sure it's in the shape of a dot. 
```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
```

## Send your dot
1. In the radio function, select the ``||radio: radio send number (0)||``. Place this under the ``||basic: show leds||``.
2. Add the ``||basic: pause (ms)||`` to the sequence. 
3. Finally, add a second ``||basic: show leds||`` and ``||basic: pause (ms)||`` as the last part of the sequence. This will create a pause between your symbols. 
```blocks
input.onButtonPressed(Button.A, function () {
    basic.showLeds(`
        . . . . .
        . # # # .
        . # # # .
        . # # # .
        . . . . .
        `)
    radio.sendNumber(0)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```

## Create your dash

This section of code for your dash is going to look almost the same as the one you just did with a few minor changes.

1. You're going to drag in a new ``||input: on button A pressed||``. Change the A to B. 
2. Add new ``||basic: show leds||`` to this sequence. Select the squares to make a dash. 
```blocks
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
```

## Send your dash
1. Next, add ``||radio: radio send number||``. Change the 0 to a 1. 
2. Add ``||basic: pause (ms)||``. 
3. Finally, add a blank ``||basic: show leds||`` and one more ``||basic: pause(ms)||`` to finish this sequence. 
```blocks
input.onButtonPressed(Button.B, function () {
    basic.showLeds(`
        . . . . .
        . . . . .
        . # # # .
        . . . . .
        . . . . .
        `)
    radio.sendNumber(1)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```

## Create your message stop
So your partner knows when your message is finished, we are going to code one more symbol doing the exact same thing as the last two sequences.
1. Drag in ``||input: on shake||``. 
2. Add new ``||basic: show leds||`` to this sequence. Select the squares to make an X. 
```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
```

## Send your message stop
1. Add ``||radio: radio send number||``. Change the 0 to a 2. 
2. Next, add ``||basic: pause(ms)||``. 
3. Finally, add blank ``||basic: show leds||`` and ``||basic: pause (ms)||`` to finish this sequence.
```blocks
input.onGesture(Gesture.Shake, function () {
    basic.showLeds(`
        # . . . #
        . # . # .
        . . # . .
        . # . # .
        # . . . #
        `)
    radio.sendNumber(2)
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
    basic.pause(100)
})
```
## Code the radio to receive messages

This last sequence of code will allow you to receive messages from your partner. Pay close attention to follow the steps below. Use the hint button if you need a visual.  

1. To start, select ``||radio: on radio received (receiveNumber)||`` and place it in your workspace. 
2. Next, select ``||logic: if true then||``. Nest this block within ``||radio: on radio received||``. 
3. You need to change the true variable in your logic function. Place ``||logic: 0=0||`` over ``||logic: true||``.
```blocks
radio.onReceivedString(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0)
```

## Receive Dot
1. Now you need to make a new ``||variable||``. Name it receivedNumber. Replace the first ``||logic: 0||`` of the function you just added with ``||variable: receivedNumber||``.
2. Within ``||logic: if…then||`` we need to add ``||basic: show leds||`` under the "if" section. Select all the leds to make a dot. 
```blocks
radio.onReceivedString(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
```
## Receive dash
Now we'll do the same for the dash.

1. Click the plus at the bottom of your ``||logic: if...then||`` block to add another condition to your variable.
2. Replace the ``||logic: true||`` variable with ``||logic: 0=0||`` and then replace the first 0 with ``||variable: receivedNumber||``. Change the second 0 to a 1. 
3. Add a second ``||basic: show leds||`` to your sequence. Select the squares to make a dash. 
```blocks
radio.onReceivedString(function (receivedNumber) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    } else if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
```
## Receive stop
And finally, we'll do the same thing for the stop. 

1. Click the plus once again to add another ``||logic: if...then||`` block. Add the ``||logic: 0=0||`` block and replace the first 0 with ``||variable: receivedNumber||``. Change the second 0 to a 2.
2. Add ``||basic: show leds||`` and select the squares to make your X symbol.
3. The very last step is to add ``||basic: pause (ms)||`` and a blank ``||basic: show leds||``.   
```blocks
radio.onReceivedString(function (receivedString) {
    let receivedNumber = 0
    if (receivedNumber == 0) {
        basic.showLeds(`
            . . . . .
            . # # # .
            . # # # .
            . # # # .
            . . . . .
            `)
    } else if (receivedNumber == 1) {
        basic.showLeds(`
            . . . . .
            . . . . .
            . # # # .
            . . . . .
            . . . . .
            `)
    } else if (receivedNumber == 2) {
        basic.showLeds(`
            # . . . #
            . # . # .
            . . # . .
            . # . # .
            # . . . #
            `)
    }
    basic.pause(100)
    basic.showLeds(`
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        . . . . .
        `)
})
```
### One Last Step

Congratulations, you have completed the Code Breaker activity. Now it's time to send some secret messages!
1. Download your code by saving it locally
2. Drag your save .hex file to your Micro:bit (make sure it is plugged in with your USB). 
3. Unplug the micro:bit from the computer and add the battery pack. 
4. Try it out against another player who also has a coded micro:bit in the same radio group.   
