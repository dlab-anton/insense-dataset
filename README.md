# Insense
Data collection repository for the Insense meditation app.


# Meditation Format
Each meditation is stored as JSON object with the following structure:

```
{
	"startTime": integer,						//	Time when the meditation started in milliseconds since Unix epoch
	"endTime": integer,							//	Time when the meditation ended in milliseconds since Unix epoch
	"duration": integer,						//	Duration of the meditation in milliseconds
	"senseStats": {
		"mind": integer,						//	Number of times the user selected the Mind sense
		"feel": integer,						//	Number of times the user selected the Feel sense
		"see": integer,							//	Number of times the user selected the See sense
		"hear": integer,						//	Number of times the user selected the Hear sense
		"think": integer,						//	Number of times the user selected the Think sense
		"mentalImage": integer,					//	Number of times the user selected the Mental Image sense
		"emotion": integer						//	Number of times the user selected the Emotion sense
	},
	"senses": base64,							//	Base64 encoded byte array with all the senses selected during the meditation session
	"moodAtTheEnd": integer,					//	User's mood at the end of the meditation session
												//	-1 = Worse, 0 = Same, 1 = Better

	"meditationType": integer,					//	Type of meditation
												//	1 = Noting, 2 = Feel Breath, 3 = Focus Mixed, 4 = Speed Noting 

	"meditationLabelType": integer				//	Label of meditation
												//	1 = Essential, 2 = Shinzen, 3 = ThreeOuter, 4 = OnlyFeel, 5 = InhaleExhale
												
	"inputMode": integer						//	Input type of meditation
												//	1 = Tap, 2 = Swipe, 3 = TimerOnly, 4 = Voice
}
```

Note: **endTime** is **NOT** guaranteed to be **startTime** + **duration** because the meditation can be paused.

# Senses Format
Senses are stored as a base64 encoded byte array with the following structure:

```
The first 8 bytes of the array store an unsigned integer representing the number of senses.
For each sense:
	* 8 byte unsigned integer -> sense type
	* 8 byte unsigned integer -> timestamp in milliseconds since Unix epoch
	* 8 byte unsigned integer -> timestamp in milliseconds since beginging of meditation
	* 8 byte unsigned integer -> number of modifiers

	For each modifier:
		* 8 byte unsigned integer -> modifier type
		* 8 byte unsigned integer -> timestamp in milliseconds since Unix epoch
		* 8 byte unsigned integer -> timestamp in milliseconds since meditation start time
```

**Senses**

```
0: Mind
1: Feel
2: See
3: Hear
4: Think
5: MentalImage
6: Emotion
7: OtherThanFeel
8: Inhale
9: Exhale
```

**Modifiers**

```
0: None
1: Past
2: Future
3: Good
4: Bad
5: NoTime
6: Neutral
7: Gone
```

# License
This dataset is provided under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode).