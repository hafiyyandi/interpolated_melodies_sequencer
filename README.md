# interpolated_melodies_sequencer

![alt text](https://static.wixstatic.com/media/a544de_4798e6cf9929408796735cde3c964c32~mv2.png/v1/fill/w_630,h_229,al_c,usm_0.66_1.00_0.01/a544de_4798e6cf9929408796735cde3c964c32~mv2.png)
See [live app](https://www.hafiyyandi.com/interpolated-melodies)
Inspired by Brian Eno’s Music for Airports & Teropa’s [Latent Cycles](https://codepen.io/teropa/full/rdoPbG/)
Code was adapted from Torin Blankensmith’s [Melody Mixer](https://github.com/googlecreativelab/melody-mixer/tree/master/demo_3)

IM Sequencer interpolates 2 melodies into 8 different sequences, each sequence similar to the sequences next to it. User can create generative music via clicking each tile and phasing in/out the different-yet-similar loops.

## Generating interpolations of 2 melodies
Uses Magenta’s [MusicVAE.js](https://tensorflow.github.io/magenta-js/music/classes/_music_vae_model_.musicvae.html)
musicVAE.interpolate([MELODY1, MELODY2], numInterpolations);
    })
 * Each interpolation contains objects with properties of pitch, start and end time.
 * The code derives the start time and duration for each note, and stores these into two arrays (for melody and baseline).
 * The durations for baseline notes are multiplied by 2.

## Creating 2 Synths
Uses [PolySynth & MembraneSynth from Tone.js](https://tonejs.github.io/docs/r13/PolySynth)
 * Melody synth: PolySynth with oscillator consisting of 0,2,4,6 partials
 * Baseline synth: MembraneSynth from the second lowest octave

## Generate independent loop for each interpolation
Uses [Tone.Part from Tone.js](https://tonejs.github.io/docs/r13/Part)
 * A Tone.Part object contains its own timeline, but the global time has to be started using Tone.Transport.start();
 * initialize_Parts() uses the constructor of Tone.Part, which needs a synth, chromatic note value (C, D, E, etc.), time, and duration. The constructor automatically creates a series of triggerAttackRelease functions from an array of note sequences.

## Play notes
Uses [p5.js](https://p5js.org/reference/)
 * Instantiate tiles
 * When a tile is clicked, play the corresponding Tone.Part loop
 * Stop when the same tile is clicked.
