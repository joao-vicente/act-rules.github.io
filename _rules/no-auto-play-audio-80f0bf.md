---
id: 80f0bf
name: Video or audio has no auto-play audio.
rule_type: composite
description: |
    This rule checks that auto-play audio does not last for more than 3 seconds, or the audio has a control mechanism to stop or mute the it.
accessibility_requirements:
  wcag20:1.4.2: # Audio Control (A)
    forConformance: true
    failed: not satisfied
    passed: further testing needed
    inapplicable: further testing needed
input_rules:
  - 95e043
  - aaa1bf
authors:
  - Anne Thyme Nørregaard
  - Bryn ANderson
---

## Applicability

This rule applies to any HTML `<audio>`, `<video>` or `<source>` elements, with a `src` attribute referencing content with a duration of more than 3 seconds, that has an `autoplay` attribute equal to `true`, and that has both `paused` and `muted` attributes equal to `false`.

## Expectation

For each test target, the outcome of at least one of the following rules is passed:
- [Auto-play audio does not last more than 3 seconds](https://act-rules.github.io/rules/aaa1bf)
- [Audio-only as a media alternative for text](https://act-rules.github.io/rules/95e043)
 
## Assumptions

*There are currently no assumptions*

## Accessibility Support

The native `<video>` and `<audio>` controls in several browser and assistive technology combinations are not keyboard accessible and the `<video>` or `<audio>` element itself may not be anounced. Authors are recomended to use custom controls for keyboard navigation and cross browser accessibility support in general.

## Background

- [Success Criterion 1.4.2 Audio Control](https://www.w3.org/TR/WCAG21/#audio-control)
- [Accessible Multimedia](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/Multimedia)

## Test Cases

### Passed

#### Passed example 1

The `<audio>` element has a control mechanism.

``` html
  <audio src="../test-assets/moon-audio/moon-speech.mp3" autoplay="true" controls></audio>
```

#### Passed example 2

The `<video>` element does not play for longer than 3 seconds.

``` html
 <video autoplay="true">
  <source src="../test-assets/rabbit-video/video.mp4#t=8,10" type="video/mp4" />
  <source src="../test-assets/rabbit-video/video.webm#t=8,10" type="video/webm" />
</video>
```

### Passed example 3

The `<video>` element autoplays, and has a control mechanism.

``` html
<head>
<style>
button {color: #000;}
button:hover {cursor: pointer;	cursor: pointer; background-color: grey;  color: white;}
</style>
</head>
<body>
	<div id="video-container">
		<!-- Video -->
		<video id="video" autoplay="true">
		 <source src="https://act-rules.github.io/test-assets/rabbit-video/video.mp4" type="video/mp4">
	   	 <source src="https://act-rules.github.io/test-assets/rabbit-video/video.webm" type="video/webm" />
		</video>
		<!-- Video Controls -->
		<div id="video-controls">
			<button type="button" id="play-pause" class="play">Play</button>
			<button type="button" id="mute">Mute</button>
		</div>
	</div>
</body>
```

### Failed

#### Failed example 1

The `<audio>` element autoplays, lasts for more than 3 seconds, and does not have a control mechanism.

``` html
  <audio src="../test-assets/moon-audio/moon-speech.mp3" autoplay="true"></audio>
```

#### Failed example 2

The `<video>` element audio autoplays for longer than 3 seconds, and does not have a control mechanism.

``` html
 <video autoplay="true">
  <source src="../test-assets/rabbit-video/video.mp4" type="video/mp4" />
  <source src="../test-assets/rabbit-video/video.webm" type="video/webm" />
</video>
```

### Inapplicable

#### Inapplicable example 1

The `<video>` element audio autoplays for longer than 3 seconds, but is `muted`.

``` html
 <video autoplay="true" muted="true">
  <source src="../test-assets/rabbit-video/video.mp4" type="video/mp4" />
  <source src="../test-assets/rabbit-video/video.webm" type="video/webm" />
</video>
```

#### Inapplicable example 2

The `<video>` element has no audio output.

``` html
 <video autoplay="true">
  <source src="../test-assets/rabbit-video/silent.mp4" type="video/mp4" />
  <source src="../test-assets/rabbit-video/silent.webm" type="video/webm" />
</video>
```

#### Inapplicable example 3

The `<audio>` element does not `autoplay`.

``` html
  <audio src="../test-assets/moon-audio/moon-speech.mp3" controls></audio>
```