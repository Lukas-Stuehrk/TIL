# Speech Synthesises with Swift

[Apples example](https://developer.apple.com/documentation/avfoundation/speech_synthesis) is both more complicated than needed and still missing important information.

The most condensed version is:

```swift

// This instance needs to live longer then the function which is executing the utterance.
let synthesizer = AVSpeechSynthesizer()

func speak() {
    // This line is missing in Apple's example.
    // Without this line the app will not synthesize speech.
    try! AVAudioSession.sharedInstance().setCategory(.playback)

    let utterance = AVSpeechUtterance(string: "This is some text.")
    synthesizer.speak(utterance)
}
```

## Missing voices on iOS 16 simulators
Furthermore, Apple broke the simulator for iOS 16. It's missing all voices and won't run any speech synthesises. It works on a real device or on other simulators, e.g. iOS 15.

## Broken voices on real devices
On my personal device, some of the available voices 
([AFSpeechSynthesisesVoice](https://developer.apple.com/documentation/avfaudio/avspeechsynthesisvoice)) 
are broken. When they are used to synthesize speech, the outputted voice will be in a fallback voice and will have "technical" output before the actual speech: `speak voice name equals ...`

It's possible to programatically detect which voices are broken: Their [`audioFileSettings` property](https://developer.apple.com/documentation/avfaudio/avspeechsynthesisvoice/3141658-audiofilesettings) is an empty dictionary. For voices which actually work, this dictionary will contain some entries.
