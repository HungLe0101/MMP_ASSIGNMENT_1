# Extend - Question 2

```
2. The user interface on the RTPClient has 4 buttons for the 4 actions. If you compare this to a standard media player, such as RealPlayer or Windows Media Player, you can see that they have only 3 buttons for the same actions: PLAY, PAUSE, and STOP (roughly corresponding to TEARDOWN). There is no SETUP button available to the user. Given that SETUP is mandatory in an RTSP interaction, how would you implement that in a media player? When does the client send the SETUP? Come up with a solution and implement it. Also, is it appropriate to send TEARDOWN when the user clicks on the STOP button?
```

## Discussion

The SETUP function can be implemented when opening the GUI, after the user had invoked and provided necessary video file name (`movie.Mjpeg` in this case).

By auto invoking SETUP step, we can skip the SETUP button. User who wants to watch the video file will have to do SETUP anyway, so there is no need for manual SETUP.

That left us with only 3 buttons, with their original functions:
- PLAY (will play the video if not already playing)
- PAUSE (will stop playing video)
- STOP (send RTSP TEARDOWN to the server and close GUI)

Since SETUP step is auto invoked, that left the question of whether TEARDOWN should also be auto invoked. For this, I decided to keep it manual, given familarity with pre-existing GUI of many different media player. User will expect for there to be a STOP button to terminate the currently opened video stream.

So yes, it is still appropriate to send RTSP TEARDOWN when user presses the STOP button.

## Implementation details

With that, we have the modified states and their transitions as follows

![Modified states and their transistions, with each arrow denoting both the action the user take and the associated underlining function](README_image/modified_states.png)
