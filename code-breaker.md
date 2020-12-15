# Code Breaker

## Set radio
To send your message, first you have to set up the radio function. 
1. In the radio tab, drag in the radio set transmit power (7) block and place it in the on start block. 
2. Next, in the radio tab, select the radio set group block and place it under the first radio block.

```blocks 
radio.setTransmitPower(7)
radio.setGroup(1)
```

## Code your dot
Next you will code your dot. This will get sent to your partner. 
1. In the input tab, drag in the On Button A Pressed block and drag it in to your workspace. 
2. Under the Basics tab, drag in the Show LED block and nest it in the On Button A Pressed block. 
3. Select the squares you want to light up. Make sure it's in the shape of a dot. 
4. In the radio function, select the "radio send number (0)" block. Place this under the "show leds" block.
5. Find the "pause" block in the basic tab. Add it to the sequence. 
6. Finally, add a second "show leds" block as the last part of the sequence. This will create a pause between your symbols. 
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
})
```
## Code your dash
This section of code for your dash is going to look almost the same as the one you just did with a few minor changes.
1. You're going to drag in a new On Button A Pressed block. Change the A to B. 
2. Add a new LED block to this sequence. Select the squares to make a dash. 
3. Add a Send Radio Number block. Change the 0 to a 1. 
4. Add a pause block. 
5. Finally, add a blank LED block to finish this sequence. 
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
})
```

## Code your message stop
So your partner knows when your message is finished, we are going to code one more symbol doing the exact same thing as the last two sequences.
1. Drag in the On Shake block. 
2. Add a new LED block to this sequence. Select the squares to make an X. 
3. Add a Send Radio Number block. Change the 0 to a 2. 
4. Add a pause block. 
5. Add a blank LED block to finish this sequence.
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
})
```
## Code the radio to receive messages
This last sequence of code will allow you to receive messages from your partner. Pay close attention to follow the steps below. Use the hint button if you need a visual.  
1. To start, select the "on radio received (receiveNumber)" and place it into your workspace. 
2. Next, go to the "Logic" functions tab and select the "if true then else" block. Nest this block within the "on radio received" block. 
3. Within the "if…then" block we need to add a "show leds" block from the "Basic" functions under the "if" section of the block 
4. change the "if true then" to "if receivedNumber then". Find the "Logic" functions select the "0 = 0" comparison and place it in your work field over the "true" 
5. Place your new variable into your work space so that it replaces the first 0 in your "if….then" block.
6. Within the "if…then" block we need to add a "show leds" block from the "Basic" functions under the "if" section of the block.
7. Change the second zero so that it equals 1 by clicking the white area and typing 1.  From the "Basic" functions tab, select the "show leds" block, drag it into the "else if" field and click the squares to make your dash symbol. 
8. click the + to add the "else if" block we need. Follow the above steps to add the "0=0" block and the "receivedNumber". This time the second 0 should be changed to 2 as it is what we coded earlier. Add the "show leds" block and design your X symbol. 
```blocks
radio.onReceivedNumber(function (receivedNumber) {
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

    } else if (receivedNumber == 3) {
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