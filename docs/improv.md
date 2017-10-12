# Sharp11 Improv Module
`require('sharp11').improv`

Contains an [Improv](#improv-object) object, which can be created with [`improv.create()`](#module-create), and an [ImprovChart](#improv-chart-object) object, which can be created by invoking the [`overChart()`](#improv-over-chart) method of an [Improv](#improv-object) object.

## <a name="module"></a> Exported Functions
### <a name="module-create"></a> create `.create(settings)`
Returns an [Improv](#improv-object) object given an optional settings object.  The settings object can contain any of the following properties:
* `dissonance` - A number (0 to 1) or a numerical range.  A higher value means the improv engine is more likely to select a less common / more dissonant scale according to [scale precedence](scale.md#module-precedence).  Default value is `0.5`.
* `changeDir` - A number (0 to 1) or a numerical range.  A higher value means the improv engine is more likely to change directions while traversing up or down a scale.  The probability of changing direction is equal to the value of `changeDir`.  Default value is `0.25`.
* `jumpiness` - A number (0 to 1) or a numerical range.  A higher value means the improv engine is more likely to jump to a random note in the current scale.  The probability of jumping is equal to the value of `jumpiness`.  Default value is `0.25`.
* `rests` - A number (0 to 1) or a numerical range.  A higher value means the improv engine is more likely to insert a rest (currently the same as extending the previous note).  The probability of inserting a rest is equal to the value of `rests`.  Default value is `[0.35, 0]`.
* `rhythmicVariety` - A number (0 to 1) or a numerical range.  A higher value means the improv engine is more likely to use triplets or sixteenths rather than eighth notes.  The probabilities of the improv engine inserting a measure of triplets or a measure of sixteenth notes are each one third the value of `rhythmicVariety`.  Default value is `[0, 0.75]`.
* `useSixteenths` - A boolean.  If false, the improv engine will not use sixteenth notes and the probability of it using triplets becomes half the value of `rhythmicVariety`.  Default value is `true`.
* `onlyEighthRests` - A boolean.  If true, the improv engine will only put rests in measures of eighth notes and not in measures of triplets of sixteenth notes.  Default value is `false`.
* `range` - An array containing two [Note](note.md#note-object) objects or strings.  The improv engine will only use notes within the given range (inclusive).  Default value is `[C4, C6]`.
* `sections` - An array listing the sections of the [Chart](chart.md#chart-object) object to improvise over and in what order.  By default, it will improvise over the original song form.
* `repeat` - A number representing the number of times to repeat the form when improvising.  Default value is `1`.
* `cadence` - A boolean.  If true, the improvisation will end by returning to the first chord of the form.  Default value is `true`.

Note: Some settings can take a numerical range instead of a number.  A numerical range is given as an array containing two values.  When improvising, the improv engine starts with the value set to the first element of the array and adjusts it linearly throughout the improvisation, reaching the second value by the end of the improvisation.

### <a name="module-isImprovChart"></a> isImprovChart `.isImprovChart(object)`
Returns true if a given object is an [ImprovChart](#improv-chart-object).

## <a name="improv-object"></a> Improv Object
`Improv` objects are used to create improvisations.

### <a name="improv-over-chart"></a> overChart `.overChart(chart)`
Improvises over a [Chart](chart.md#chart-object) object returning an [ImprovChart](#improv-chart-object) object.

## <a name="improv-chart-object"></a> ImprovChart Object
An `ImprovChart` represents an improvisation over a [Chart](chart.md#chart-object).

### <a name="improv-chart-chart"></a> chart `.chart`
The [Chart](chart.md#chart-object) object being improvised over.

### <a name="improv-chart-data"></a> data `.data`
An array of objects representing the notes that have been improvised for a given chord change.  Each object contains the following properties:
* `chord` - A [Chord](chord.md#chord-object) object representing the chord change.
* `scale` - A [Scale](scale.md#scale-object) object representing the scale that was chosen for improvising over the chord change.
* `notes` - An array of beats.  Each beat is an array of two (eighth), three (triplet), or four (sixteenth) notes.  Notes can either be [Note](note.md#note-object) objects or `null`, representing rests.
* `duration` - A [Duration](duration.md#duration-object) object representing the duration of the chord change.

### <a name="improv-chart-notes-and-durations"></a> notesAndDurations `.notesAndDurations()`
Returns an array of objects representing the notes in the improvisation.  Each object has a key `note` that corresponds to a [Note](note.md#chord-object) object or `null` for a rest, and a key `duration` that corresponds to a [Duration](duration.md#duration-object) object.

### <a name="improv-chart-chords-and-durations"></a> chordsAndDurations `.chordsAndDurations()`
Returns an array of objects representing the chords in the improvisation.  Each object has a key `chord` that corresponds to a [Chord](chord.md#chord-object) object, and a key `duration` that corresponds to a [Duration](duration.md#duration-object) object.

### <a name="improv-chart-midi"></a> midi `.midi(settings)`
Returns a [Midi](midi.md#midi-object) object for the improvisation with given [`settings`](midi.md#midi-settings).
